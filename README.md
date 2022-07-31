#写在之前
项目中用到的函数简介：https://github.com/EveandBob/Introduction-to-some-functions-in-elliptic-curves-not-projects-

# 项目名称
通过签名值来获取公钥，并且来验证签名

# 项目实现
在实现该项目的过程中需要注意下面几件事

1.点压缩（需要使用求解2次剩余）

2.验证流程如下
![Screenshot 2022-07-31 123420](https://user-images.githubusercontent.com/104854836/182010280-b0183732-43c2-4153-ab46-e76d284a8118.jpg)

# 部分代码
使用签名来获得公钥
```python
 def USE_R_S_get_PA(sign, e):
        r, s = sign
        x1 = (r - e) % n
        y11,y12=get_y(x1)
        KG1=x1,y11
        KG2=x1,y12
        SG=calculate_np(Gx,Gy,s,a,b,p)
        TSG=calculate_Tp(SG[0],SG[1],a,b,p)
        num1=get_inverse(s+r,n)
        temp=calculate_p_q(KG1[0],KG1[1],TSG[0],TSG[1],a,b,p)
        PA1=calculate_np(temp[0],temp[1],num1,a,b,p)
        temp = calculate_p_q(KG2[0], KG2[1], TSG[0], TSG[1], a, b, p)
        PA2 = calculate_np(temp[0], temp[1], num1, a, b, p)

        return PA1,PA2
```

# 实验结果
![Screenshot 2022-07-31 123620](https://user-images.githubusercontent.com/104854836/182010306-398241a4-07a2-434f-8ed9-5cfece31e0e6.jpg)
