# 限制奖券导出查询时间不超过1年的实施计划

## 项目背景
在 `StoGiftCouponController` 和 `DmsGiftCouponController` 两个控制器中，都有 `export` 方法用于导出奖券数据。目前这两个方法没有对查询时间范围进行限制，可能导致用户查询过长时间段的数据，影响系统性能。现需要增加限制逻辑，确保查询时间范围不超过1年。

## 需求分析
1. 在 `StoGiftCouponController.export()` 方法中添加时间验证逻辑
2. 在 `DmsGiftCouponController.export()` 方法中添加时间验证逻辑
3. **开始时间 `createTimeBegin` 必须输入**，结束时间 `createTimeEnd` 如果不输入，默认到今天
4. 验证 `createTimeBegin` 和 `createTimeEnd` 参数之间的时间差
5. 如果时间差超过1年，返回错误提示："查询区间不能大于一年"
6. 如果开始时间大于结束时间，返回错误提示："开始时间不能大于结束时间"
7. 页面输入时间区间的格式可能有2种，`yyyy-MM-dd HH:mm:ss` 或者 `yyyy-MM-dd`，都要兼容
8. 时间验证应在执行查询之前进行

## 技术实现方案

### 方案一：在控制器层添加验证
直接在每个控制器的 export 方法中添加时间验证逻辑。

### 方案二：创建公共工具类
创建一个时间验证工具类，供两个控制器共用。

推荐使用方案一，因为代码简单且易于维护。

## 实现步骤

### 步骤1：导入必要的类
- `java.time.Period`
- `java.time.LocalDate`
- `java.time.LocalDateTime`
- `java.time.format.DateTimeFormatter`
- `java.time.format.DateTimeParseException`

### 步骤2：验证开始时间必填
检查 `createTimeBegin` 参数是否为空，如果为空则返回错误提示

### 步骤3：处理结束时间默认值
如果 `createTimeEnd` 参数为空，默认设置为今天

### 步骤4：解析时间参数（兼容两种格式）
- 尝试使用 `yyyy-MM-dd HH:mm:ss` 格式解析
- 如果失败，尝试使用 `yyyy-MM-dd` 格式解析
- 处理解析异常

### 步骤5：计算时间差
使用 `ChronoUnit.DAYS.between()` 计算两个日期之间的天数

### 步骤6：验证开始时间不能大于结束时间
如果 `startDate > endDate`，则抛出异常

### 步骤7：验证时间差
如果时间差超过365天，则抛出异常

### 步骤8：测试验证
测试各种边界情况，确保功能正常

## 代码实现要点

```java
// 示例验证逻辑
// 1. 导入 ServiceException
import com.crbr.wmhy_act.exception.ServiceException;

// 2. 验证开始时间必填
if (StringUtils.isEmpty(createTimeBegin)) {
    throw new ServiceException("开始时间不能为空");
}

// 3. 处理结束时间默认值
if (StringUtils.isEmpty(createTimeEnd)) {
    createTimeEnd = LocalDate.now().format(DateTimeFormatter.ofPattern("yyyy-MM-dd"));
}

// 4. 解析时间参数（兼容两种格式）
LocalDate startDate;
LocalDate endDate;
try {
    // 尝试解析 yyyy-MM-dd HH:mm:ss 格式
    try {
        LocalDateTime startDateTime = LocalDateTime.parse(createTimeBegin, DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss"));
        startDate = startDateTime.toLocalDate();
    } catch (DateTimeParseException e) {
        // 尝试解析 yyyy-MM-dd 格式
        startDate = LocalDate.parse(createTimeBegin, DateTimeFormatter.ofPattern("yyyy-MM-dd"));
    }

    try {
        // 尝试解析 yyyy-MM-dd HH:mm:ss 格式
        LocalDateTime endDateTime = LocalDateTime.parse(createTimeEnd, DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss"));
        endDate = endDateTime.toLocalDate();
    } catch (DateTimeParseException e) {
        // 尝试解析 yyyy-MM-dd 格式
        endDate = LocalDate.parse(createTimeEnd, DateTimeFormatter.ofPattern("yyyy-MM-dd"));
    }
} catch (Exception e) {
    throw new ServiceException("时间格式不正确，请使用 yyyy-MM-dd 或 yyyy-MM-dd HH:mm:ss 格式");
}

// 5. 验证开始时间不能大于结束时间
if (startDate.isAfter(endDate)) {
    throw new ServiceException("开始时间不能大于结束时间");
}

// 6. 计算天数差并验证
long days = java.time.temporal.ChronoUnit.DAYS.between(startDate, endDate);
if (days > 365) {
    throw new ServiceException("查询区间不能大于一年");
}
```

## 预期结果
- 当开始时间为空时，导出功能将不会执行，并返回错误提示："开始时间不能为空"
- 当结束时间为空时，默认使用今天作为结束时间
- 当开始时间大于结束时间时，导出功能将不会执行，并返回错误提示："开始时间不能大于结束时间"
- 当查询时间范围超过1年时，导出功能将不会执行，并返回错误提示："查询区间不能大于一年"
- 当查询时间范围在1年内时，导出功能正常执行
- 当时间格式不正确时，返回错误提示："时间格式不正确，请使用 yyyy-MM-dd 或 yyyy-MM-dd HH:mm:ss 格式"
- 系统性能得到保护，避免因查询大数据量导致的问题

## 风险评估
- 时间格式解析可能出现异常，需做好异常处理
- 需要确保时间比较逻辑正确，避免闰年等特殊情况的影响
- 需要测试各种时间格式输入，确保兼容性

## 测试案例
1. **开始时间为空**：应拒绝导出并返回错误信息："开始时间不能为空"
2. **结束时间为空**：应默认使用今天作为结束时间，正常执行导出
3. **查询范围为1年整**：应允许导出
4. **查询范围超过1年**：应拒绝导出并返回错误信息："查询区间不能大于一年"
5. **时间格式为 yyyy-MM-dd**：应正常解析并执行导出
6. **时间格式为 yyyy-MM-dd HH:mm:ss**：应正常解析并执行导出
7. **时间格式不正确**：应返回错误信息："时间格式不正确，请使用 yyyy-MM-dd 或 yyyy-MM-dd HH:mm:ss 格式"
8. **开始时间大于结束时间**：应返回适当的错误信息