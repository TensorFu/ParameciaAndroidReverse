```javascript
function main() 
{
    Java.perform(function x() 
    {
        console.log("java perform");
        var stringClass = Java.use("java.lang.String");
        var verfiy = Java.use('org.teamsik.ahe17.qualification.Verifier');
        var p = stringClass.$new('09042ec2c2c08c4cbece042681caf1d13984f24a');
        var pSign = p.getBytes();
        console.log(bytesToString(pSign));

        for (var i = 7000; i < 10000; i++) 
        {
            console.log(i);
            var v = String(i);
            var vSign = verfiy.encodePassword(v);
            if (bytesToString(vSign) == bytesToString(pSign)) 
            {
                console.log("real vSign:" + v);
                break;
            }
        }
    });

    function bytesToString(arr) 
    {
        var str = '';
        arr = new Uint8Array(arr);
        for (var i in arr) {
            str += String.fromCharCode(arr[i]);
        }
        return str;
    }
}
```

`var p = stringClass.$new('09042ec2c2c08c4cbece042681caf1d13984f24a');`  新建一个java的string的数据类型

或者是这样

`var pass = Java.use('java.lang.String').$new('/5B++P65NK44NNROl0wNOLLLL=');`



`var pSign = p.getBytes();` 将这个java数据类型的p转换成bytes数据类型



```javascript
 // ByteString.of是用来把byte[]数组转成hex字符串的函数, Android系统自带ByteString类
 var ByteString = Java.use("com.android.okhttp.okio.ByteString");
 var j = Java.use("c.business.comm.j");
 j.x.implementation = function() {
     var result = this.x();
     console.log("j.x:", ByteString.of(result).hex());
     return result;
 };
 
 j.a.overload('[B').implementation = function(bArr) {
     this.a(bArr);
     console.log("j.a:", ByteString.of(bArr).hex());
 };   
```

```javascript
//ByteString.of是用来把byte[]数组转成hex字符串的函数, Android系统自带ByteString类
var j = Java.use("c.business.comm.j")
j.a.overload('[B').implementation = function(bArr) {
     this.a(bArr);
     console.log("j.a:", ByteString.of(bArr).hex());
 }; 
```





