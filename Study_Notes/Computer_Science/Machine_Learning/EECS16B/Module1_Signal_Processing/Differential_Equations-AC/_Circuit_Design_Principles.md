# Design Principle*
## Design Principle
> Note 7 Fa21
> 




## Choosing Cutoff Frequency
> Note 6 Fa21
> 




# Design Examples
## Finding Resistors
> **Hw05 Fa21 P5**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688222993293-8c5d0bd6-fa43-41ba-a4ec-82ee90573b83.png#averageHue=%23f1efec&clientId=u8b3d18e2-5f95-4&from=paste&id=u2ee52461&originHeight=1529&originWidth=1495&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=658687&status=done&style=none&taskId=ub387c9be-a2dc-4be2-bc4b-e06d996867b&title=)

**(a) Finding Resistor for low pass filter**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688223056246-e06b92b1-7a6e-47d1-ad9d-3d2bfa5d7a18.png#averageHue=%23fefefe&clientId=u8b3d18e2-5f95-4&from=paste&id=u4b208a0f&originHeight=740&originWidth=1397&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=46542&status=done&style=none&taskId=u1460c9b3-2ed3-41a7-be81-d4d396ca20f&title=)
**(b) Finding Resistor for high pass filter**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688223081543-76f83a27-dfb9-4f96-940d-0dbf642af051.png#averageHue=%23ffffff&clientId=u8b3d18e2-5f95-4&from=paste&id=u8bbd60a4&originHeight=304&originWidth=1367&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=43728&status=done&style=none&taskId=ua0a6f8d0-f156-48bb-98c1-fdc707226a0&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688223093051-971701de-6f32-4115-ae7c-5f35d84bd577.png#averageHue=%23fefefe&clientId=u8b3d18e2-5f95-4&from=paste&id=u1e7c9508&originHeight=421&originWidth=1364&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=12748&status=done&style=none&taskId=u3192b00a-01c0-4450-a8f3-2463f0f96c9&title=)
**(c) Composing Filters with OpAmp Unity Buffer**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688223119783-26b88f43-3e5d-45c8-8cdb-b73311b445bc.png#averageHue=%23fefefe&clientId=u8b3d18e2-5f95-4&from=paste&id=u042e9a46&originHeight=1158&originWidth=1403&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=145790&status=done&style=none&taskId=u27d501bf-bf0d-4324-8395-fbb1a96fd17&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688223145305-3fbd519f-9421-469a-b2c4-2d27cea08e59.png#averageHue=%23fcfcfc&clientId=u8b3d18e2-5f95-4&from=paste&id=u1f595549&originHeight=1135&originWidth=1551&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=124220&status=done&style=none&taskId=ua121050f-7946-4019-9df6-31cab24a3e2&title=)
**(d) Output Analysis**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688223156579-dff2ea80-9727-4278-b0f9-ebf8b376b2c6.png#averageHue=%23ffffff&clientId=u8b3d18e2-5f95-4&from=paste&id=u7c12a3f9&originHeight=357&originWidth=1415&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=44618&status=done&style=none&taskId=u4d7b0219-305a-4c6f-b2ca-b41b4f4e0bf&title=)


## Infer Circuit Elements⭐⭐⭐⭐⭐
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688223405267-a0b5426b-ecb3-4697-b595-5a1e48c29a3d.png#averageHue=%23f9f8f7&clientId=u8b3d18e2-5f95-4&from=paste&id=uc66b0b02&originHeight=1778&originWidth=1390&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=413698&status=done&style=none&taskId=uda5d42f1-bcb6-4858-b90e-07b339af522&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688223412432-7934d1ac-7560-4be6-8feb-aa7ee241a105.png#averageHue=%23f9f8f7&clientId=u8b3d18e2-5f95-4&from=paste&id=u1a3a4452&originHeight=124&originWidth=1402&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=26859&status=done&style=none&taskId=ufb0b4575-dd8e-4560-9fad-f22b6f474da&title=)

**(a) Inverting Amplifier in Phasor Domain**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688223437356-e53fbf00-2c97-4094-a3d0-06371790b098.png#averageHue=%23ffffff&clientId=u8b3d18e2-5f95-4&from=paste&id=uc69cebec&originHeight=197&originWidth=1568&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=34736&status=done&style=none&taskId=u92f80758-1e7c-467d-8dfa-323d8551f00&title=)
**(b) Infer Z1 and Z2**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688223919942-faf18afc-8ad8-40d3-8058-0d8bf5ce50a2.png#averageHue=%23ffffff&clientId=u285b58e4-2405-4&from=paste&id=uec7d3a14&originHeight=665&originWidth=1576&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=147461&status=done&style=none&taskId=ue74f7dc7-7aba-428d-8657-c7ed1a0b0f7&title=)
**(c) Infer Z2's Value**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688223992313-ffc4b3d7-0ea2-4906-9a60-de7de1cc3369.png#averageHue=%23ffffff&clientId=u285b58e4-2405-4&from=paste&id=u6128758a&originHeight=99&originWidth=1602&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=34075&status=done&style=none&taskId=u2a95828c-327e-4561-9830-c69c828777f&title=)
**(d) Infer Z1's Value**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688224001435-19a17b5b-b2e4-4226-8f98-cc87df1b5462.png#averageHue=%23ffffff&clientId=u285b58e4-2405-4&from=paste&id=ubf052363&originHeight=817&originWidth=1657&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=79126&status=done&style=none&taskId=u6bcc0e40-2273-43f1-9a4f-3f2c5a569ea&title=)

# Resources
> Note 6/7 Fa21

