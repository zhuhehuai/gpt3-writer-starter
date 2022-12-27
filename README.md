### 在作业中遇到的问题
如果你跟我一样是电脑小白，那就从最简单的地方开始吧。
### 1.准备工作
安装👉[Node.js](https://nodejs.org/en/)：一个可以让你的电脑运行JavaScript代码的工具。(JavaScript 是一种用来编写网页应用程序和网站的编程语言。)

安装👉[Windows PowerShell](https://learn.microsoft.com/zh-cn/powershell/scripting/install/installing-powershell?view=powershell-7.3)：一种任务自动化和配置管理程序。它由命令行shell和相关脚本语言组成。（Shell是一种电脑程序，它可以让你输入指令，处理一些任务，比如复制文件，启动程序等等。它有点像一个小机器人，它会按照你的指令去做事情。）

安装👉[Visual Studio Code](https://code.visualstudio.com/):一款免费编辑器，它可以帮助你编写和修改代码。

### 2.打开[教程](https://buildspace.so/p/build-ai-writing-assistant-gpt3/lessons/clone-repo-settle-on-an-idea)
在建立你自己的分支以后，在桌面，或者你用来放练习的地方，新建一个文件夹，命名最好是用英文，中文容易出bug，复制路径。

![image](https://user-images.githubusercontent.com/65635084/209671724-a934dbbb-358a-4c1c-9883-2ce99e625042.png)


打开PowerShell，输入`cd`（cd=更改路径） ，按一下空格，然后`Ctrl+V`粘贴提前复制好的路径，按下回车键`enter`

![image](https://user-images.githubusercontent.com/65635084/209672305-489d1d6f-077f-4edc-ae5e-fc0d92bceee3.png)

然后输入 `git clone https://github.com/zhuhehuai/gpt3-writer-starter/` 将代码下载到指定文件夹。用这种方法，你可以在任意的文件夹，拷贝Github上各种代码。


![image](https://user-images.githubusercontent.com/65635084/209673111-1601aced-57fe-4c4c-ad6b-55d7f172531c.png)

``` 
    //切换到刚才下载好的gpt3-writer-starter文件夹
    👇
    cd gpt3-writer-starter

    //安装next react react-dom
    （Yarn add next react react-dom是安装 Next.js、React 和 React-dom 的命令行命令，
      Next.js 是一种用于构建 React 应用程序的框架，
      React 是一种用于构建用户界面的 JavaScript 库，
      React-dom 是专门用于在浏览器上渲染 React 组件的库。）
    👇
    yarn add next react react-dom

    //运行程序
    （Yarn dev是一个yarn命令，它可以帮助你在开发环境中启动应用程序。
     Yarn是一个Facebook开发的JavaScript包管理器，用于安装、升级、配置和删除Node.js包。）
    👇
    yarn dev
``` 
到这一步，你大概率是能打开做练习用的网页了。https://localhost:3000
接下来进入代码修改环节。

打开 Visual Studio Code ，英文差的同学可以先把界面调成中文的。

通过快捷键`Ctrl+Shift+P`，打开命令面板，输入`configure display language`，切换到中文。

打开 gpt3-writer-starter 文件夹，然后就可以愉快的改代码了！

![image](https://user-images.githubusercontent.com/65635084/209677513-31a6333d-b574-4a3a-8533-a041e5c7608e.png)

最后附上一份作业，供参考

``` 

import Head from 'next/head'; 
import Image from 'next/image'; 
import buildspaceLogo from '../assets/buildspace-logo.png'; 
import { useState } from 'react'; 

//这段代码中，首先使用了next/head模块，它可以在页面头部添加一些元素，比如标题、描述等。
  然后使用next/image模块，它可以帮助我们优化图片的加载性能，并将图片按指定的格式加载到页面中。
  最后，使用了react的useState hook，它可以帮助我们在函数式组件中管理状态。

  
const Home = () => {
  const [userInput, setUserInput] = useState('');
  const [apiOutput, setApiOutput] = useState('')
  const [isGenerating, setIsGenerating] = useState(false)
  
//JavaScript 中的 const 关键字用于声明不能更改或重新分配的变量。
  当你使用 const Home = () => {} 时，它声明了一个可以全局访问的匿名函数，但它的值不能更改或重新分配。
  这段代码中，使用了React hooks中的useState函数，它可以帮助我们在函数式组件中管理状态。
  userInput、apiOutput和isGenerating变量都是用来存储状态信息的，可以用来根据用户输入，调用API，获取相应结果，并设置相应变量
  
const callGenerateEndpoint = async () => {
  setIsGenerating(true);
  
  //JavaScript 中的 const 关键字用于声明不能更改或重新分配的变量。
  在此示例中，const callGenerateEndpoint 是一个使用 async/await 语法将布尔标志设置为 true 的函数。
  此标志用于指示端点当前正在生成，当端点生成完成时它将设置为 false。这是异步编程中常用的模式，用于指示某些任务的进度。
  
  console.log("Calling OpenAI...")
  const response = await fetch('/api/generate', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({ userInput }),
  });
  
  //此代码使用 console.log() 函数将一条消息记录到控制台，表明它正在调用 OpenAI API。
  然后它使用 fetch() API 向 /api/generate 端点发出 POST 请求。
  此请求包括一个包含用户输入的正文，该正文在发送前被字符串化。然后将响应存储在响应变量中，并可用于检索请求的结果。

  const data = await response.json();
  const { output } = data;
  console.log("OpenAI replied...", output.text)

  setApiOutput(`${output.text}`);
  setIsGenerating(false);
}

//此代码使用 const 关键字声明一个名为 data 的变量，并将其设置为等于来自使用 fetch() API 的 API 调用的响应。
然后它使用解构来访问记录到控制台的响应数据的输出。
最后调用setApiOutput()函数将输出文本设置为字符串，调用setIsGenerating()函数将布尔标志设置为false，表示端点生成完成。

  const onUserChangedText = (event) => {
  console.log(event.target.value);
  setUserInput(event.target.value);
};

//此代码使用 const 关键字创建一个名为 onUserChangedText 的函数。
此函数将事件对象作为参数，并使用 console.log() 函数将事件对象的目标属性值记录到控制台。
然后它使用 setUserInput() 函数将 userInput 状态变量设置为事件对象的目标属性的值。
当用户在输入字段中键入内容时，此函数用于更新 userInput 状态变量。

  return (
    <div className="root">
      <Head>
        <title>GPT-3 Writer | buildspace</title>
      </Head>
      <div className="container">
        <div className="header">
          <div className="header-title">
            <h1>猫娘模拟器</h1>
          </div>
          <div className="header-subtitle">
            <h2>喵~</h2>
          </div>
        </div>
        
        //此代码呈现一个类名为“根”的分区，并包含一个用于设置页面标题的首页组件和一个类名为“容器”的 分区。
        在容器分区中，有一个类名为“标头”的分区，其中包含另外两个分区。
        第一个分区包含一个带有文本“猫娘模拟器”的 h1 标签，第二个分区包含一个带有文本“喵~”的 h2 标签。
        此代码创建一个带有标题和副标题的简单页眉。
        
        <div className="prompt-container">
          <textarea
            className="prompt-box"
            placeholder="愚蠢的主人，想干什么呢？"
            value={userInput}
            onChange={onUserChangedText}
          />;
           <div className="prompt-buttons">
           <a
              className={isGenerating ? 'generate-button loading' : 'generate-button'}
              onClick={callGenerateEndpoint}
            >
              <div className="generate">
              {isGenerating ? <span className="loader"></span> : <p>发送消息</p>}
              </div>
            </a>
           </div>
           
           //这段代码渲染了一个类名为“提示容器”的分区，其中包含一个类名为“提示框”的文本区域元素和占位符文本“愚昧的主人，想干什么呢？”。
           文本区域元素设置为用户输入状态变量的值，变化时事件设置为 onUserChangedText 函数（）。
           在 提示容器 分区内部是一个类名为“提示按钮”的分区，
           其中包含一个类名为“生成按钮”的标记和一个设置为 callGenerateEndpoint 函数的点击事件。
           a 标签包含一个带有 className“generate”的分区，其中包含一个带有 className“加载”的 span 和 ap 标签。
           span 和 p 标签根据 isGenerating 状态变量有条件地呈现。此代码创建一个文本输入字段和一个按钮。
           
           {apiOutput && (
              <div className="output">
                <div className="output-header-container">
                  <div className="output-header">
                    <h3>回复消息</h3>
                  </div>
                </div>
                <div className="output-content">
                  <p>{apiOutput}</p>
                </div>
              </div>
            )}
          </div>
      </div>
      
      //此代码呈现一个条件呈现的分区，其类名为“output”，其中包含两个分区，
      一个类名为“output-header-container”的分区和一个类名为“output-content”的分区。
      output-header-container分区包含一个带有文本“回复消息”的 h3 标签，
      output-content分区包含呈现 apiOutput 状态变量的 ap 标签。此代码创建一个输出容器，该容器根据 apiOutput 状态变量有条件地呈现。
      
      <div className="badge-container grow">
        <a
          href="https://buildspace.so/builds/ai-writer"
          target="_blank"
          rel="noreferrer"
        >
          <div className="badge">
            <Image src={buildspaceLogo} alt="buildspace logo" />
            <p>build with buildspace</p>
          </div>
        </a>
      </div>
    </div>
  );
};

//此代码呈现一个类名为“badge-container grow”的分区，其中包含一个标签，其中 href 属性设置为构建空间网站，
目标属性设置为“_blank”，rel 属性设置为“noreferrer”。
在 a 标签内是一个类名为“徽章”的分区，它包含一个 Image 组件，其 src 属性设置为 buildspaceLogo 变量，
alt 属性设置为“buildspace logo”和带有文本“build with buildspace”的 ap 标签。此代码创建一个链接到构建空间网站的徽章。

export default Home;

//这段代码是一个 export 语句，它从当前模块导出 Home 组件，允许它被其他模块使用。此语句使 Home 组件可用于从其他文件导入。


``` 


