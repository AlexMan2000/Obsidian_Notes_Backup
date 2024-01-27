# Circuit Analysis in Phasor Domain
## Principles
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687491646202-387c5e5f-2742-4339-bd31-825114fc4317.png#averageHue=%23f6f4f2&clientId=ubb32db90-495a-4&from=paste&id=ua8e2b2b4&originHeight=633&originWidth=1492&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=247853&status=done&style=none&taskId=uaf8f6372-397d-4f43-8832-71ec7b020e3&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687491655484-04e92dc5-37fe-4067-8b3a-8840db622dd4.png#averageHue=%23faf9f8&clientId=ubb32db90-495a-4&from=paste&id=u3ee6834b&originHeight=865&originWidth=1561&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=183795&status=done&style=none&taskId=ua05307cd-a5b6-48bd-8c5b-501511c3aa8&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687491667157-07cff5af-6f64-4bba-a14f-5f91f7caf1e3.png#averageHue=%23fbfaf9&clientId=ubb32db90-495a-4&from=paste&id=u4c1e3f38&originHeight=1238&originWidth=1389&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=282021&status=done&style=none&taskId=ucd0dd8b4-0422-4236-92c6-40123052d32&title=)



## Comparison
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1685592418819-50245aa7-7420-4211-bd39-73d73f09b7d3.png#averageHue=%23fbfbfa&clientId=ub67c7d7d-fbda-4&from=paste&id=Cx6AM&originHeight=555&originWidth=1527&originalType=binary&ratio=1.5625&rotation=0&showTitle=false&size=64599&status=done&style=none&taskId=uba98c2f8-b526-4773-b23e-d775ed88644&title=)
> 由上文我们知道，$v_C(t)=2 \mathrm{e}^{-200 t}+(\sin (200 t)-\cos (200 t)) \mathrm{V}=2e^{-200t}+\sqrt{2}cos(200t-\frac{3\pi }{4})$
> 于是当$t\to \infty$时，$v_C(t)=\sqrt{2}cos(200t-\frac{3\pi }{4})$, 是电路的稳定状态的解。
> 如果我们使用`Phasor Analysis`呢?
> $v_{in}(t)=2*\frac{e^{j200t}-e^{-j200t}}{2j}=-je^{200t}+je^{-j200t}$, $w=200 \frac{rad}{s}$
> 于是$\widetilde{V_{in}}=-j$, $H(jw)=\frac{\frac{1}{jwC}}{\frac{1}{jwC}+R}=\frac{1}{1+j}$, 于是$\widetilde{V_{out}}=H(jw)\widetilde{V_{in}}=\frac{1}{j-1}=\frac{\sqrt{2}}{2}e^{-j\frac{3}{4}\pi}$, 即$B=\frac{\sqrt{2}}{2}$,$\phi=-\frac{3}{4}\pi$。
> 利用`Inverse Phasor Transform`可得$v_c(t)=2\times\frac{\sqrt{2}}{2}cos(wt+\phi)=\sqrt{2}cos(200t-\frac{3\pi}{4})$。
> 所以使用`Phasor Analysis`得到的结果就是`Steady State Solution of the circuit`。



## Working Examples
### Example 1: Cosine Wave Input
> **This example is from Note 6 Fa21**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687491837107-1e287f90-b969-45ef-b933-b87d9390ddba.png#averageHue=%23faf9f9&clientId=ubb32db90-495a-4&from=paste&id=ud8f9ec92&originHeight=1143&originWidth=1487&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=244034&status=done&style=none&taskId=u700b3fcd-f34c-4841-a063-37552d387a9&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687491850985-a321eda9-074d-4f69-9acf-b1ccb843c6fd.png#averageHue=%23fcfbfb&clientId=ubb32db90-495a-4&from=paste&id=uf6249819&originHeight=1208&originWidth=1136&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=213762&status=done&style=none&taskId=uf8ac2d69-7171-4711-8a31-55f617856b4&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687491860306-c4c9d278-0dc9-401e-ae83-b879f70b0ea6.png#averageHue=%23fbf9f7&clientId=ubb32db90-495a-4&from=paste&id=u7e8e74c1&originHeight=818&originWidth=1102&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=200257&status=done&style=none&taskId=u2e3f187c-029f-410e-a554-d9fcf754227&title=)

**Important Footnotes**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687491901887-491bdfd1-1e27-4cd6-aa9f-d8dd3d880f40.png#averageHue=%23faf8f6&clientId=ubb32db90-495a-4&from=paste&id=u5c049dad&originHeight=123&originWidth=1110&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=40811&status=done&style=none&taskId=uc580f88b-c4f6-4076-8202-c271ac1b17e&title=)


### Example 2: Sine Wave Input
> **This example is from disc4B Fa21**
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687530079540-f70426a1-0be5-429b-bfa1-7e21b0d19bd6.png#averageHue=%23fcfcfc&clientId=ufc72584d-464c-4&from=paste&height=553&id=u398b5d50&originHeight=829&originWidth=1798&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=87832&status=done&style=none&taskId=u23607cee-9927-4009-8924-9e5feaad308&title=&width=1198.6666666666667)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687530091214-1510b393-2562-4149-ba20-ef7c99da5fed.png#averageHue=%23f8f7f6&clientId=ufc72584d-464c-4&from=paste&height=58&id=uff8c68de&originHeight=87&originWidth=1779&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=26992&status=done&style=none&taskId=uace551e2-e18f-425c-9f73-1bedaf28a7e&title=&width=1186)

**Step 1: Write Source as Exponentials**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687530111794-e7a3a86f-88d5-4a26-a2da-5f5f79a9b46d.png#averageHue=%23f2f1ef&clientId=ufc72584d-464c-4&from=paste&id=u1e32395e&originHeight=254&originWidth=1760&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=101384&status=done&style=none&taskId=ud62ecf8a-1ad8-4ee5-97b4-1326ce0f13e&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687530120682-d4bd0b8f-272c-4d88-a672-abd8dc4148ef.png#averageHue=%23fefefe&clientId=ufc72584d-464c-4&from=paste&id=u9bf20004&originHeight=914&originWidth=1354&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=122526&status=done&style=none&taskId=u5dfb5363-0c99-4a58-9f74-8e0fc0ba4f8&title=)
**Step 2: Transform Circuit into Phasor Domain**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687530169169-2eabb43d-7ace-4692-b7b6-81502205f4fb.png#averageHue=%23f9f8f7&clientId=ufc72584d-464c-4&from=paste&id=ud539ea32&originHeight=523&originWidth=1397&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=137144&status=done&style=none&taskId=uba3f6952-4897-41d5-b7e2-594e2e11f4f&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687530177350-4dbb03b3-83da-434a-bfdf-db603e92363f.png#averageHue=%23fcfcfc&clientId=ufc72584d-464c-4&from=paste&id=ud4e9ca5e&originHeight=938&originWidth=1371&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=110868&status=done&style=none&taskId=u37017425-f2dc-43a2-a0f6-d03210ca98c&title=)
**Step 3: Compute Quantities in Phasor Domain**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687530210681-ef4ff940-1a52-4689-87e5-d6d1abe7ed93.png#averageHue=%23fbfafa&clientId=ufc72584d-464c-4&from=paste&id=uc733be5e&originHeight=1105&originWidth=1321&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=268462&status=done&style=none&taskId=uc61a8388-f4df-428a-b57a-f79f84a760a&title=)
**Step 4: Fit in the Values and Solve the Equations**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687530252493-b46fcd29-ee81-4407-82ad-92e6a0d24792.png#averageHue=%23fefdfd&clientId=ufc72584d-464c-4&from=paste&id=u05663498&originHeight=1278&originWidth=1047&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=189146&status=done&style=none&taskId=u7473aec3-d2a8-4faf-9fde-cd0defcb8bb&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687530267160-d3ebabb6-f013-4b4a-960e-01182d3cfc04.png#averageHue=%23fefefe&clientId=ufc72584d-464c-4&from=paste&id=u6505cef2&originHeight=1024&originWidth=1076&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=102941&status=done&style=none&taskId=uaba4c490-00ba-4921-a19c-1c629b4d07c&title=)
**Step 5: Transform Back to the Time Domain**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1687530285884-70461bb1-0b3c-4fbb-b954-128c0a0efa7c.png#averageHue=%23fbfaf9&clientId=ufc72584d-464c-4&from=paste&id=u75983bee&originHeight=366&originWidth=1029&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=93583&status=done&style=none&taskId=u764605df-e9ee-4fc0-9ac0-29081c035d5&title=)


### Example 3: General Input  
> ![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688210802306-54742e40-00a2-4564-9e9b-d68e135e0722.png#averageHue=%23fbfbfa&clientId=u06910da5-f620-4&from=paste&id=u78b514bd&originHeight=1094&originWidth=1699&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=184631&status=done&style=none&taskId=u2e83646c-4f1b-4362-99cc-65a85374024&title=)

**Solution**![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688219316993-a240d010-7e56-4636-aea0-c9c56a332006.png#averageHue=%23ffffff&clientId=u06910da5-f620-4&from=paste&id=u8b6b360b&originHeight=1193&originWidth=1688&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=282469&status=done&style=none&taskId=u37ab8c60-fe53-4ba9-a3b9-f85443d4b8d&title=)![image.png](https://cdn.nlark.com/yuque/0/2023/png/12393765/1688219327220-487ecbb6-9acb-4ba5-9892-264946d46f19.png#averageHue=%23ffffff&clientId=u06910da5-f620-4&from=paste&id=u2e87517c&originHeight=355&originWidth=1705&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=101734&status=done&style=none&taskId=u262f5d61-fd80-4ecb-bb91-18303c137ea&title=)
> 对于任意常数输入，我们也可以将其看作是



# *AC Equivalence
> 





# *AC Power
> 





