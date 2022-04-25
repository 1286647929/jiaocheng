**背景**: 最近羊毛没啥好写的了,京东也慢慢薅不动了(blog也鸽🕊了好久了呢),最近也有人问我脚本的问题,这里就统一写一个基础的脚本教程,给大家抛砖引玉,做一个基础基础!(本人小白水平,其中有啥错误 ❎ ,也希望各位大佬指教 )

## **一 : 梳理思路：**

1. 想要签到 , 必须有一个可以签到的软件 , 网页 , 小程序等
2. [抓包](https://www.wangan.com/p/7fygfgd3e50bbcae) 你想要进行签到的 软件 , 网页 , 小程序等(不会抓包或抓不到包的点击[抓包](https://www.wangan.com/p/7fygfgd3e50bbcae) 的超链接去学习)
3. 然后就是分析(很有可能需要解密的相关知识)你抓的数据包 , 直到找到 **签到** (或其他操作) 包
4. 使用测试工具进行测试,确定是否可以请求成功(不成功自己寻找并解决问题)直到可以成功请求
5. 最后就是写脚本了, 只要前面的完成了, 写脚本那就很快了

## 二: 思路有了, 那就开始吧!

> 博主是小白 博主是小白 博主是小白 博主是小白 博主是小白
>
> 有任何错误笑笑就好了 , 当然更加欢迎您指出我的错误 , 万分感激的!

### 首先确定一个目标(今天来个简单的例子🌰)

微信小程序:骁友会 (直接搜索或扫码进入:扫码有邀请 没啥用的,在意的自己搜索)

- [![image-20220411213118940](https://yml-img.ml:521/images/2022/04/11/image-20220411213118940.png)](https://yml-img.ml:521/images/2022/04/11/image-20220411213118940.png)
- 注册登录后可以找到 **任务列表** 里面有 **每日签到** 跟其他的很多任务(今天就搞这个签到)
- 然后就是下一步了

### 进行 **签到** (相关操作)的抓包

#### 根据不同的机型 , 我们需要分类讨论了 首先来说说ios吧

- ios 抓包相关
  - 抓包软件
    - 免费的 : stream 图标就是个心电图是的 , 免费软件 , 国区可自行下载
    - 收费软件:
      1. 不得不说的就是 **[圈x](https://www.kejiwanjia.com/jiaocheng/zheteng/notes/21016.html)** ios绕不开的软件 , 操作教程找科技玩家小姐姐(点击超链接即可)(不会告诉你我搬运到我的bolg了) , 需要自行外区下载
      2. thor 也叫锤子 , 就是长得像索尔的🔨吧 , 需要自行外区下载 (有这个软件的应该不需要教程)
      3. Http Catcher 也叫网球 🎾 ,可能就是长得像🎾吧 国区可下载 , 高级功能需要付费解锁 🔓 , 有这个软件的也不需要教程
      4. 别的没怎么用过 , 听说过了
  - 抓包操作
    - 不同的软件 , 操作也有所差异 , 但是本质都是一样的 , 都是通过建立 vpn 进行代理网络流量 , 从而进行捕获数据包 . 想要捕获https 数据包 , 都需要进行证书的信任工作 , 记得有两个关于证书的操作就够了,一个地方安装证书 , 一个地方信任证书 ; 详细教程自己百度 , google 去吧!

#### Android 抓包相关

- 相对比 ios 来说 , 安卓的抓包就有利有弊了,得益于安卓的生态,也毁在安卓的生态(个人见解哈)
  - 抓包软件
    - 小黄鸟(3.3.6) , 小蓝鸟 , 还有各种小黄鸟的改版 ; 安卓端知名的抓包软件 , 推荐3.3.6版本,别问为啥
    - 抓包精灵 跟小黄鸟差不多的
    - 还有好多好多好多好多没听说过的软件
- 抓包操作 同ios 自行搜索研究去吧!

#### PC 抓包相关

- 上面的软件基本都是基于手机的 , 总有这样那样的不方便的地方,个人觉得还是配合电脑抓包,才能更好 , 更更快的分析数据包 (当然,你只有手机就当我在💨)
- PC 抓包软件推荐
  1. **Fiddler** 首推fd,mac的话可以考虑 **charles** , fd的强大是人尽皆知的:学习链接 – [52破解基础基础](https://www.52pojie.cn/forum.php?mod=viewthread&tid=1171662&highlight=Fiddler) [进阶教程](https://www.52pojie.cn/home.php?mod=space&uid=1075167&do=thread&view=me&order=dateline&from=space&page=2)
  2. **charles** （也叫花瓶、青花瓷等）mac用户首推这个 , 当然win也有这个 分类很好用; [看雪charles教程](https://zhuanlan.kanxue.com/article-13139.htm)
  3. 别的没怎么用过 , 当然抓包工具还有超级多的

#### 抓包签到

- 打开你的抓包软件 , 或者手机连上你的电脑抓包软件
- 确定开始正常抓包后去app执行签到相关操作
- 返回抓包工具 , 停止抓包 , 备注刚才抓包的app 进行的操作(不能备注的也没办法)
- 至此,抓包结束 🔚

### 分析刚才抓的数据包

> 分析数据包这个东西吧 , 没法教 ,主要看自己的悟性(就是猜) , 自己的英语水平 (数据包基本没有中文,只有部分中文的提示,基本全是英语) , 还有就是自己的经验(废话) ,我们一点点来说吧！

#### 首先可以根据 **url** 链接,寻找关键字进行定位 📌 (就是有根据的瞎猜)

- 例如: 某个url如下

- `https://qualcomm.growthideadata.com/qualcomm-app/api/user/signIn?userId=xxx` 请你判断下这个url 是做什么工作的 用户登录

- 我们来分析下这个

   

  url

  1. 首先前面是固定的 `https://` 这个是 **https** 请求
  2. `qualcomm.growthideadata.com` 是他的域名(也就是host)
  3. `/user/signIn` 很明显就是`/用户/登录` 了鸭

- 像这种的根据 **url** 中的英文单词来判断 这个数据包功能是 非常非常非常 常见的,因为你第一眼看到的就是这玩意了

#### 然后我们还可以根据 **响应体** 来进行判断 (请求头 请求体 响应头 响应体还不懂的自行去补课: [简书](https://www.jianshu.com/p/eb3e5ec98a66) )

- 例如: 某个响应体如下 ;

```
JAVASCRIPT
{
  "code": 0,
  "message": "success！",
  "data": {
    "coins": 5
  }
}
```

- 请你判断下这个 响应体 可能是什么的 , 我们经常用的数据有哪些? 点击我查看答案

#### 我们可以根据数据包的类型来进行初步筛选

- 一般请求都是 `post` 或者 `get` 请求 , 我们根据数据包类型减少工作量
- 一般有携带账号密码信息的请求都是使用 `post` 进行的
- 一些简单的请求可能使用 `get`

#### 我们可以根据获得的数据进行搜索筛选

- 例如: 我们签到获得了5 积分 , 我们就可以直接搜索 `5` 作为关键字搜索响应体(因为这个数据是服务器发回我们的,所以搜索响应体) ; 搜索出来数据可能超级多 因为 `5` 太常见了 ; 如果 `33` `78` 等这样的值这样搜索 效果比较好
- 同理，也可以进行中文的搜索筛选（效果非常不理想，很多返回都是英文的）

#### 可以通过软件内的时间来进行辅助定位

- 例如：你签到成功后，很多软件都会给你一个积分（金币）啥的明细表，就是你什么时间，做了什么操作，然后获得了多少积分等
- 可以根据软件给的时间 来进行辅助定位，很多软件会精确到毫秒 ，所以这不失为一个好方法呢(o)/~

#### 没有别的办法那就只能查看所有数据包，慢慢寻找你要的数据包了

- 找的过程也要慢慢积累，尽可能的搞清楚他的命名逻辑，对以后的找包速度会有明显提升

#### 下面给出本次试验对象的签到数据包

- [![image-20220411213118940](https://raw.githubusercontent.com/1286647929/jiaocheng/ee568f41a08b18ae6c802a0a83b7bba155c6cf10/-1.jpg)](https://raw.githubusercontent.com/1286647929/jiaocheng/ee568f41a08b18ae6c802a0a83b7bba155c6cf10/-1.jpg)

### 使用测试工具进行测试

> 其实这里我不知道该叫什么名字，反正我就按照我自己的理解进行教程，有不对，不合适的地方，请指出

#### 使用抓包工具自带的软件进行测试

- 很多抓包工具都带有数据包

   

  重发

   

  功能，例如：

  - 安卓：小黄鸟、小蓝鸟
  - ios：圈x自带重放 锤子配合 anubis 网球没用过
  - pc： fd自带重放 花瓶（charles）都可以直接进行重放

- 一般当你不能确定是否是这条数据包时，重放总是一个不错的选择！

#### 使用第三方的调试工具进行测试

- 我比较常用的有 **postman** **apipost**等
- 这里主要是进行数据的重放与必要参数的测试

#### 进行数据包参数测试

- 这一步主要是确定服务器会校验那些参数，那也就是我们写脚本必须要加强关注的参数
- 所谓的服务器校验，也就是你发送过去后 他会判断这个参数是否正常，不正常的话一般会返回一些错误码等等
- 也就是说，你要保证他检验的数据一定是正确的，你才有可能签到（别的什么操作）成功
- 得到最简的参数时，这一步可以算完成了

### 接下来就是最后一步了，我们开始写脚本吧

> 开始写脚本之前我先声明几句
>
> 1. 我的js是自学的，难免有错误的地方
> 2. 很多地方都是大佬的开源脚本修改的，可能修改的四不像，但是我用着舒服就行了
> 3. 脚本我写了很多注释 // 就是双引号后面的内容，希望可以帮你可以尽快的理解这一行的作用
> 4. 有任何不懂得地方，直接百度、google查一下 很快就懂了
> 5. 没了没了 开始

- 首先，脚本地址：[链接](https://github.com/1286647929/jiaocheng/blob/614944d5c757be0896fff96b08982f4353141d8e/jiaocheng.js)
- 如果遇到任何问题，请首尝试自己解决它，这样你的成长才会更快；实在解决不了的可以群里问
- 啰啰嗦嗦几千字了，第一版就先这样吧
- 下面给懒得同学吧脚本内容搬运下，省的跳过去看了！

```js
JAVASCRIPT
/**
 * 教程 
 * 地址： https://raw.githubusercontent.com/yml2213/template/master/jiaocheng.js
 * 
 * 教程    这里是写脚本说明的地方
 * 本脚本仅用于学习使用请勿直接运行
 * 
 * ========= 青龙 =========
 * 变量格式：export jiaocheng_data=' xxxx & xxx @  xxxx & xxx '  多个账号用 @分割 
 * 
 */

const jsname = "教程";
const $ = Env(jsname);
const notify = $.isNode() ? require('./sendNotify') : '';      // 这里是 node（青龙属于node环境）通知相关的
const Notify = 1; //0为关闭通知，1为打开通知,默认为1
const debug = 1; //0为关闭调试，1为打开调试,默认为0
//////////////////////
let jiaocheng_data = process.env.jiaocheng_data;               // 这里是 从青龙的 配置文件 读取你写的变量
let jiaocheng_dataArr = [];
let data = '';
let msg = '';


!(async () => {

	if (!(await Envs()))  	//多账号分割 判断变量是否为空  初步处理多账号
		return;
	else {

		console.log(`本地脚本4-11 )`);       // console.log是输出信息的，可以在脚本日志中看到输出（打印）的信息

		console.log(`\n\n=========================================    \n脚本执行 - 北京时间(UTC+8)：${new Date(
			new Date().getTime() + new Date().getTimezoneOffset() * 60 * 1000 +
			8 * 60 * 60 * 1000).toLocaleString()} \n=========================================\n`);

		await wyy();

		console.log(`\n=================== 共找到 ${jiaocheng_dataArr.length} 个账号 ===================`)

		if (debug) {
			console.log(`【debug】 这是你的全部账号数组:\n ${jiaocheng_dataArr}`);
		}


		for (let index = 0; index < jiaocheng_dataArr.length; index++) {


			let num = index + 1
			console.log(`\n========= 开始【第 ${num} 个账号】=========\n`)

			data = jiaocheng_dataArr[index].split('&');      // 这里是分割你每个账号的每个小项   

			if (debug) {
				console.log(`\n 【debug】 这是你第 ${num} 账号信息:\n ${data}\n`);
			}


			// 这里是开始做任务    需要注意的点
			// 	1. await只能运行与async函数中
			// 	2. 函数的名字不可以相同
			//      3. 不够可以自己复制

			console.log('开始 xx');
			await signin();
			await $.wait(2 * 1000);

			// 这里是开始做任务   
			console.log('开始 yy');
			await yyyy();
			await $.wait(2 * 1000);


			// 这里是开始做任务   
			console.log('开始 zz');
			await zzzzz();
			await $.wait(2 * 1000);



			await SendMsg(msg);    // 与发送通知有关系
		}
	}

})()
	.catch((e) => console.logErr(e))
	.finally(() => $.done())






/**
 * 签到  骁友会
 * 下面我们来看看函数需要注意的东西吧
 */
function signin(timeout = 3 * 1000) {
	return new Promise((resolve) => {
		let url = {
			url: `https://qualcomm.growthideadata.com/qualcomm-app/api/user/signIn?userId=${data[1]}`,    // 这是请求的 url 可以直接用我们抓包、精简后的URL
			headers: {            // headers 是请求体  可以直接用精简后的 hd  也就是服务器校验的部分，他需要啥，我们就给他啥  

				"userId": data[1],
				"Content-Type": "application/x-www-form-urlencoded;charset=UTF-8",
				"Host": "qualcomm.growthideadata.com",
				"User-Agent": UA,
				"sessionKey": data[0],
				"Referer": "https://servicewechat.com/wx026c06df6adc5d06/176/page-frame.html",
				"Connection": "keep-alive"
			},
			// body: '',       // 这是一个 get 请求，没有请求体 body   如果是 post 不要忘记他鸭！

		}

		if (debug) {
			console.log(`\n【debug】=============== 这是 签到 请求 url ===============`);
			console.log(JSON.stringify(url));
		}

		$.get(url, async (error, response, data) => {     // 这是一个 get 请求 , 如果是 post  记得把这里改了 
			try {
				if (debug) {
					console.log(`\n\n【debug】===============这是 签到 返回data==============`);
					console.log(data)
				}

				let result = JSON.parse(data);
				if (result.code == 200) {        // 这里是根据服务器返回的数据做判断  方便我们知道任务是否完成了

					console.log(`【签到】${result.message} 🎉 `)
					msg += `\n【签到】${result.message} 🎉`

				} else if (result.code === 1) {    // 这里是根据服务器返回的数据做判断  方便我们知道任务是否完成了

					console.log(`\n【签到】 失败 ,可能是:${result.message}!\n `)


				} else if (result.code === 40001) {   // 这里是根据服务器返回的数据做判断  方便我们知道任务是否完成了

					console.log(`\n【签到】 失败 ,可能是:${result.message}!\n `)


				} else {    // 这里是根据服务器返回的数据做判断  方便我们知道任务是否完成了

					console.log(`\n【签到】 失败 ❌ 了呢,可能是网络被外星人抓走了!\n `)


				}

			} catch (e) {
				console.log(e)
			} finally {
				resolve();
			}
		}, timeout)
	})
}




// 如果有更多的需求，直接复制上一个函数，改个名   然后稍微更改一下内容   就可以用了   
// 不要忘记与上面的 函数调用对应起来鸭














//#region 固定代码 可以不管他
// ============================================变量检查============================================ \\
async function Envs() {
	if (jiaocheng_data) {
		if (jiaocheng_data.indexOf("@") != -1) {
			jiaocheng_data.split("@").forEach((item) => {
				jiaocheng_dataArr.push(item);
			});
		} else {
			jiaocheng_dataArr.push(jiaocheng_data);
		}
	} else {
		console.log(`\n 【${$.name}】：未填写变量 jiaocheng_data`)
		return;
	}

	return true;
}

// ============================================发送消息============================================ \\
async function SendMsg(message) {
	if (!message)
		return;

	if (Notify > 0) {
		if ($.isNode()) {
			var notify = require('./sendNotify');
			await notify.sendNotify($.name, message);
		} else {
			$.msg(message);
		}
	} else {
		console.log(message);
	}
}

/**
 * 随机数生成
 */
function randomString(e) {
	e = e || 32;
	var t = "QWERTYUIOPASDFGHJKLZXCVBNM1234567890",
		a = t.length,
		n = "";
	for (i = 0; i < e; i++)
		n += t.charAt(Math.floor(Math.random() * a));
	return n
}

/**
 * 随机整数生成
 */
function randomInt(min, max) {
	return Math.round(Math.random() * (max - min) + min)
}

//每日网抑云
function wyy(timeout = 3 * 1000) {
	return new Promise((resolve) => {
		let url = {
			url: `https://keai.icu/apiwyy/api`
		}
		$.get(url, async (err, resp, data) => {
			try {
				data = JSON.parse(data)
				console.log(`\n 【网抑云时间】: ${data.content}  by--${data.music}`);

			} catch (e) {
				console.logErr(e, resp);
			} finally {
				resolve()
			}
		}, timeout)
	})
}

//#endregion


// prettier-ignore   固定代码  不用管他
function Env(t, e) { "undefined" != typeof process && JSON.stringify(process.env).indexOf("GITHUB") > -1 && process.exit(0); class s { constructor(t) { this.env = t } send(t, e = "GET") { t = "string" == typeof t ? { url: t } : t; let s = this.get; return "POST" === e && (s = this.post), new Promise((e, i) => { s.call(this, t, (t, s, r) => { t ? i(t) : e(s) }) }) } get(t) { return this.send.call(this.env, t) } post(t) { return this.send.call(this.env, t, "POST") } } return new class { constructor(t, e) { this.name = t, this.http = new s(this), this.data = null, this.dataFile = "box.dat", this.logs = [], this.isMute = !1, this.isNeedRewrite = !1, this.logSeparator = "\n", this.startTime = (new Date).getTime(), Object.assign(this, e), this.log("", `🔔${this.name}, 开始!`) } isNode() { return "undefined" != typeof module && !!module.exports } isQuanX() { return "undefined" != typeof $task } isSurge() { return "undefined" != typeof $httpClient && "undefined" == typeof $loon } isLoon() { return "undefined" != typeof $loon } toObj(t, e = null) { try { return JSON.parse(t) } catch { return e } } toStr(t, e = null) { try { return JSON.stringify(t) } catch { return e } } getjson(t, e) { let s = e; const i = this.getdata(t); if (i) try { s = JSON.parse(this.getdata(t)) } catch { } return s } setjson(t, e) { try { return this.setdata(JSON.stringify(t), e) } catch { return !1 } } getScript(t) { return new Promise(e => { this.get({ url: t }, (t, s, i) => e(i)) }) } runScript(t, e) { return new Promise(s => { let i = this.getdata("@chavy_boxjs_userCfgs.httpapi"); i = i ? i.replace(/\n/g, "").trim() : i; let r = this.getdata("@chavy_boxjs_userCfgs.httpapi_timeout"); r = r ? 1 * r : 20, r = e && e.timeout ? e.timeout : r; const [o, h] = i.split("@"), n = { url: `http://${h}/v1/scripting/evaluate`, body: { script_text: t, mock_type: "cron", timeout: r }, headers: { "X-Key": o, Accept: "*/*" } }; this.post(n, (t, e, i) => s(i)) }).catch(t => this.logErr(t)) } loaddata() { if (!this.isNode()) return {}; { this.fs = this.fs ? this.fs : require("fs"), this.path = this.path ? this.path : require("path"); const t = this.path.resolve(this.dataFile), e = this.path.resolve(process.cwd(), this.dataFile), s = this.fs.existsSync(t), i = !s && this.fs.existsSync(e); if (!s && !i) return {}; { const i = s ? t : e; try { return JSON.parse(this.fs.readFileSync(i)) } catch (t) { return {} } } } } writedata() { if (this.isNode()) { this.fs = this.fs ? this.fs : require("fs"), this.path = this.path ? this.path : require("path"); const t = this.path.resolve(this.dataFile), e = this.path.resolve(process.cwd(), this.dataFile), s = this.fs.existsSync(t), i = !s && this.fs.existsSync(e), r = JSON.stringify(this.data); s ? this.fs.writeFileSync(t, r) : i ? this.fs.writeFileSync(e, r) : this.fs.writeFileSync(t, r) } } lodash_get(t, e, s) { const i = e.replace(/\[(\d+)\]/g, ".$1").split("."); let r = t; for (const t of i) if (r = Object(r)[t], void 0 === r) return s; return r } lodash_set(t, e, s) { return Object(t) !== t ? t : (Array.isArray(e) || (e = e.toString().match(/[^.[\]]+/g) || []), e.slice(0, -1).reduce((t, s, i) => Object(t[s]) === t[s] ? t[s] : t[s] = Math.abs(e[i + 1]) >> 0 == +e[i + 1] ? [] : {}, t)[e[e.length - 1]] = s, t) } getdata(t) { let e = this.getval(t); if (/^@/.test(t)) { const [, s, i] = /^@(.*?)\.(.*?)$/.exec(t), r = s ? this.getval(s) : ""; if (r) try { const t = JSON.parse(r); e = t ? this.lodash_get(t, i, "") : e } catch (t) { e = "" } } return e } setdata(t, e) { let s = !1; if (/^@/.test(e)) { const [, i, r] = /^@(.*?)\.(.*?)$/.exec(e), o = this.getval(i), h = i ? "null" === o ? null : o || "{}" : "{}"; try { const e = JSON.parse(h); this.lodash_set(e, r, t), s = this.setval(JSON.stringify(e), i) } catch (e) { const o = {}; this.lodash_set(o, r, t), s = this.setval(JSON.stringify(o), i) } } else s = this.setval(t, e); return s } getval(t) { return this.isSurge() || this.isLoon() ? $persistentStore.read(t) : this.isQuanX() ? $prefs.valueForKey(t) : this.isNode() ? (this.data = this.loaddata(), this.data[t]) : this.data && this.data[t] || null } setval(t, e) { return this.isSurge() || this.isLoon() ? $persistentStore.write(t, e) : this.isQuanX() ? $prefs.setValueForKey(t, e) : this.isNode() ? (this.data = this.loaddata(), this.data[e] = t, this.writedata(), !0) : this.data && this.data[e] || null } initGotEnv(t) { this.got = this.got ? this.got : require("got"), this.cktough = this.cktough ? this.cktough : require("tough-cookie"), this.ckjar = this.ckjar ? this.ckjar : new this.cktough.CookieJar, t && (t.headers = t.headers ? t.headers : {}, void 0 === t.headers.Cookie && void 0 === t.cookieJar && (t.cookieJar = this.ckjar)) } get(t, e = (() => { })) { t.headers && (delete t.headers["Content-Type"], delete t.headers["Content-Length"]), this.isSurge() || this.isLoon() ? (this.isSurge() && this.isNeedRewrite && (t.headers = t.headers || {}, Object.assign(t.headers, { "X-Surge-Skip-Scripting": !1 })), $httpClient.get(t, (t, s, i) => { !t && s && (s.body = i, s.statusCode = s.status), e(t, s, i) })) : this.isQuanX() ? (this.isNeedRewrite && (t.opts = t.opts || {}, Object.assign(t.opts, { hints: !1 })), $task.fetch(t).then(t => { const { statusCode: s, statusCode: i, headers: r, body: o } = t; e(null, { status: s, statusCode: i, headers: r, body: o }, o) }, t => e(t))) : this.isNode() && (this.initGotEnv(t), this.got(t).on("redirect", (t, e) => { try { if (t.headers["set-cookie"]) { const s = t.headers["set-cookie"].map(this.cktough.Cookie.parse).toString(); s && this.ckjar.setCookieSync(s, null), e.cookieJar = this.ckjar } } catch (t) { this.logErr(t) } }).then(t => { const { statusCode: s, statusCode: i, headers: r, body: o } = t; e(null, { status: s, statusCode: i, headers: r, body: o }, o) }, t => { const { message: s, response: i } = t; e(s, i, i && i.body) })) } post(t, e = (() => { })) { if (t.body && t.headers && !t.headers["Content-Type"] && (t.headers["Content-Type"] = "application/x-www-form-urlencoded"), t.headers && delete t.headers["Content-Length"], this.isSurge() || this.isLoon()) this.isSurge() && this.isNeedRewrite && (t.headers = t.headers || {}, Object.assign(t.headers, { "X-Surge-Skip-Scripting": !1 })), $httpClient.post(t, (t, s, i) => { !t && s && (s.body = i, s.statusCode = s.status), e(t, s, i) }); else if (this.isQuanX()) t.method = "POST", this.isNeedRewrite && (t.opts = t.opts || {}, Object.assign(t.opts, { hints: !1 })), $task.fetch(t).then(t => { const { statusCode: s, statusCode: i, headers: r, body: o } = t; e(null, { status: s, statusCode: i, headers: r, body: o }, o) }, t => e(t)); else if (this.isNode()) { this.initGotEnv(t); const { url: s, ...i } = t; this.got.post(s, i).then(t => { const { statusCode: s, statusCode: i, headers: r, body: o } = t; e(null, { status: s, statusCode: i, headers: r, body: o }, o) }, t => { const { message: s, response: i } = t; e(s, i, i && i.body) }) } } time(t, e = null) { const s = e ? new Date(e) : new Date; let i = { "M+": s.getMonth() + 1, "d+": s.getDate(), "H+": s.getHours(), "m+": s.getMinutes(), "s+": s.getSeconds(), "q+": Math.floor((s.getMonth() + 3) / 3), S: s.getMilliseconds() }; /(y+)/.test(t) && (t = t.replace(RegExp.$1, (s.getFullYear() + "").substr(4 - RegExp.$1.length))); for (let e in i) new RegExp("(" + e + ")").test(t) && (t = t.replace(RegExp.$1, 1 == RegExp.$1.length ? i[e] : ("00" + i[e]).substr(("" + i[e]).length))); return t } msg(e = t, s = "", i = "", r) { const o = t => { if (!t) return t; if ("string" == typeof t) return this.isLoon() ? t : this.isQuanX() ? { "open-url": t } : this.isSurge() ? { url: t } : void 0; if ("object" == typeof t) { if (this.isLoon()) { let e = t.openUrl || t.url || t["open-url"], s = t.mediaUrl || t["media-url"]; return { openUrl: e, mediaUrl: s } } if (this.isQuanX()) { let e = t["open-url"] || t.url || t.openUrl, s = t["media-url"] || t.mediaUrl; return { "open-url": e, "media-url": s } } if (this.isSurge()) { let e = t.url || t.openUrl || t["open-url"]; return { url: e } } } }; if (this.isMute || (this.isSurge() || this.isLoon() ? $notification.post(e, s, i, o(r)) : this.isQuanX() && $notify(e, s, i, o(r))), !this.isMuteLog) { let t = ["", "==============📣系统通知📣=============="]; t.push(e), s && t.push(s), i && t.push(i), console.log(t.join("\n")), this.logs = this.logs.concat(t) } } log(...t) { t.length > 0 && (this.logs = [...this.logs, ...t]), console.log(t.join(this.logSeparator)) } logErr(t, e) { const s = !this.isSurge() && !this.isQuanX() && !this.isLoon(); s ? this.log("", `❗️${this.name}, 错误!`, t.stack) : this.log("", `❗️${this.name}, 错误!`, t) } wait(t) { return new Promise(e => setTimeout(e, t)) } done(t = {}) { const e = (new Date).getTime(), s = (e - this.startTime) / 1e3; this.log("", `🔔${this.name}, 结束! 🕛 ${s} 秒`), this.log(), (this.isSurge() || this.isQuanX() || this.isLoon()) && $done(t) } }(t, e) }
```

## 你竟然还能看到这里

- 没想到你竟然还能看到这里，那不点击一下下面的赞赏？
- 偷偷告诉你 赞赏的点击彩蛋 我能玩一天
- 不信试试吧!
