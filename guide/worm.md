# 保留策略/对象锁定（WORM）

US3保留策略具有WORM（Write Once Read Many）特性，满足用户以不可删除、不可篡改方式保存和使用数据。如果您希望指定时间内任何用户（包括资源拥有者）均不能修改和删除US3某个Bucket中的Object，您可以选择为Bucket配置保留策略。在保留策略指定的Object保留时间到期之前，仅支持在Bucket中上传和读取Object。Object保留时间到期后，才可以修改或删除Object。

## 使用场景

US3保留策略支持的WORM特性（对象锁定功能）是用于勒索软件防护的对象存储不可变性的行业标准，适用于金融、保险、医疗、证券、日志数据等保审查等场景。

## 设置bucket保留策略

选择对应空间，在右侧操作中选择开启保留策略按钮。

![](/images/guide/bucket锁定开启1.png)

设置保留策略，选择保留时间，设置完成后，点击确定按钮，完成保留策略设置。

![](/images/guide/bucket锁定开启2.png)

成功后效果如下

![](/images/guide/bucket锁定开启3.png)

后续上传的Object，会自动应用保留策略。

## 设置对象保留策略

在对象列表页，选择对应对象，在右侧操作中选择保留策略按钮。

![](/images/guide/对象锁定1.png)

设置保留策略，选择保留时间，保留时间到期后，才可以修改或删除Object。

![](/images/guide/对象锁定2.png)

设置完成后，点击确定按钮，完成保留策略设置。

## 使用场景（worm保留策略生效时间怎么生效呢？）

1. 2024年12月1日在bucket上设置保留策略为10天。
2. file2.txt文件分别在2024年12月2日以及在2025年1月2日上传过两个版本,版本号分别为(version2/version3),不同版本间的保留时间为上传的时间+bucket上设置的保留天数。
3. 单独设置file4.txt保留到2025年3月14日

|              |   文件创建时间  |   文件保留时间  |  版本号 | 是否单独设置文件保留时间 |
| ------------ | ------------- | ------------- | ------------- | ------------- |
| file1.txt    | 2024年11月19日 |    不保留      |  | 否 |
| file2.txt    | 2024年12月2日  | 2024年12月12日 | version1 | 否 |
| file2.txt    | 2025年1月2日   | 2025年1月12日  | version2 | 否 |
| file3.txt    | 2025年2月2日   | 2025年2月12日  |  | 否 |
| file4.txt    | 2025年2月2日   | 2025年3月14日  |  | 2025年3月14日|

## 注意事项

1. bucket级别的保留策略，设置后只对bucket下新上传的文件有效，对历史文件不生效。
2. bucket级别的保留策略，设置后不支持关闭，如果要取消保留策略，更新保留时间为0天。
3. 保留策略设置后，Object保留时间到期前，仅支持上传和读取Object，不支持修改和删除Object（包括元数据）。
4. 对象级别的保留策略，设置后不支持关闭或者取消，只支持延长保留期。
5. 保留策略依赖于版本控制特性，需要开启版本控制特性后，才能使用保留策略。
6. 配置保留策略后，版本控制不可暂停。