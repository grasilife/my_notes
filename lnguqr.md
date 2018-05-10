# readyState详解



| readyState 状态 | 状态说明 |
| --- | --- |
| (0)未初始化 | 此阶段确认XMLHttpRequest对象是否创建，并为调用open()方法进行未初始化作好准备。值为0表示对象已经存在，否则浏览器会报错－－对象不存在。 |
| (1)载入 | 此阶段对XMLHttpRequest对象进行初始化，即调用open()方法，根据参数(method,url,true)完成对象状态的设置。并调用send()方法开始向服务端发送请求。值为1表示正在向服务端发送请求。 |
| (2)载入完成 | 此阶段接收服务器端的响应数据。但获得的还只是服务端响应的原始数据，并不能直接在客户端使用。值为2表示已经接收完全部响应数据。并为下一阶段对数据解析作好准备。 |
| (3)交互 | 此阶段解析接收到的服务器端响应数据。即根据服务器端响应头部返回的MIME类型把数据转换成能通过responseBody、responseText或responseXML属性存取的格式，为在客户端调用作好准备。状态3表示正在解析数据。 |
| (4)完成 | 此阶段确认全部数据都已经解析为客户端可用的格式，解析已经完成。值为4表示数据解析完毕，可以通过XMLHttpRequest对象的相应属性取得数据。 |

<span data-type="color" style="color: rgb(75, 75, 75);"><span data-type="background" style="background-color: rgb(255, 255, 255);">概而括之，整个XMLHttpRequest对象的生命周期应该包含如下阶段：</span></span>
<span data-type="color" style="color: rgb(75, 75, 75);"><span data-type="background" style="background-color: rgb(255, 255, 255);">创建－初始化请求－发送请求－接收数据－解析数据－完成</span></span>
```javascript

            const getJSON = function (url) {
                const promise = new Promise(function (resolve, reject) {
                    const handler = function () {
                        var states = ["正在初始化……", "正在初始化请求……成功！<br/>正在发送请求……",
                            "成功！<br/>正在接收数据……",
                            "完成！<br/>正在解析数据……",
                            "完成！<br/>"
                        ];
                        console.log(this, states[this.readyState])
                        if (this.readyState !== 4) {
                            return;
                        }
                        if (this.status === 200) {
                            resolve(this.response);
                        } else {
                            reject(new Error(this.statusText));
                        }
                    };
                    const client = new XMLHttpRequest();
                    client.open("GET", url);
                    client.onreadystatechange = handler;
                    client.responseType = "json";
                    client.setRequestHeader("Accept", "application/json");
                    client.send();

                });

                return promise;
            };

            getJSON("/").then(function (json) {
                console.log('Contents: ' + json);
            }, function (error) {
                console.error('出错了', error);
            });
```

