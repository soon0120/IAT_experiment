### 1  实验简介：内隐联想测验

**内隐联想测验（Implicit Association Test，IAT）**，由Anthony Greenwald等人于1998年首次提出，是一种心理测验工具，用于评估个体对特定概念或群体的内隐态度和潜在偏见。其基本原理：如果某个概念与某个属性在个体的心中存在紧密的联结，那么个体在将它们归类在一起时会反应得更快。

------

### 2  实验设计

**内群体（ingroup）**指的是个体认为自己属于的群体，**外群体（outgroup）**指的是个体不认为自己属于的群体。人们通常对内群体有更积极的态度，而对外群体可能持有更多的负面态度或偏见。这种现象被称为“内群体偏好”，这种偏好可能是显性的或内隐的。因此，本教程设计一个简单的IAT实验去揭示个体对内外群体的潜在态度或偏见。

#### 2.1  实验材料

##### 2.1.1  概念图片

本实验中，内外群体分别选自亚裔群体和白人群体。从Chicago Face Database中选取图片16张，其中亚裔群体图片8张（男女各半），白人群体图片8张（男女各半）。

![asian1.jpg](https://s2.loli.net/2024/07/30/chBWjNGEpz1mRXx.jpg)

<center>
    图1（内外群体例图，如亚裔女性）
</center>

![white2.jpg](https://s2.loli.net/2024/07/30/xOVzsB1MyNdmkIn.jpg)

<center>
    图2（内外群体例图，如白人男性）
</center>

##### 2.1.2  属性词汇

本实验中，选取积极词汇和消极词汇各8个。其中积极词汇包括：愉快、和平、美好、善良、光荣、成功、坚韧、乐观；消极词汇包括：苦恼、糟糕、肮脏、邪恶、失败、伤害、悲观、沮丧。

#### 2.2  实验流程

一般情况下，一个内隐联想测验实验包含5个阶段：概念分类、属性分类、联合任务一、概念反向分类、联合任务二阶段。

##### 2.2.1  阶段一：概念图片分类

本阶段，被试需要对内（亚裔群体）外（白人群体）群体进行辨别分类。屏幕中央会依次呈现一系列群体图片，要求被试看见亚裔图片按 “E” 键，白人图片按 “I” 键。如果被试判断错误，图片下方会出现一个红叉，提示被试修正自己的按键判断。在被试做出正确判断后，再进入下一个试次。

##### 2.2.2  阶段二：属性词汇分类

本阶段，被试需要对积极词汇和消极词汇进行辨别分类。屏幕中央会依次呈现一系列属性词汇，要求被试看见积极词汇按 “E” 键，消极词汇按 “I” 键。如果被试判断错误，词汇下方会出现一个红叉，提示被试修正自己的按键判断。在被试做出正确判断后，再进入下一个试次。

##### 2.2.3  阶段三：联合任务一（属性词汇&概念图片分类）

本阶段，被试需要同时对内（亚裔）外（白人）群体以及积极和消极词汇进行辨别分类。屏幕中央会依次呈现一系列的群体图片和属性词汇，要求被试亚裔图片或积极词汇按 “E” 键，白人图片或消极词汇按 “I” 键。如果被试判断错误，图片下方会出现一个红叉，提示被试修正自己的按键判断。在被试做出正确判断后，再进入下一个试次。

##### 2.2.4  阶段四：概念图片反向分类

本阶段，被试需要再次对内（亚裔）外（白人）群体进行辨别分类，不过按键是发生了变化的。要求被试看见白人图片按 “E” 键，亚裔图片按 “I” 键。依旧，若被试判断错误，图片下方会出现一个红叉，提示被试修正自己的按键判断。在被试做出正确判断后，再进入下一个试次。

##### 2.2.5  阶段五：联合任务二（属性词汇&概念图片反向分类）

本阶段，被试又需要同时对内（亚裔）外（白人）群体以及积极和消极词汇进行辨别分类。要求被试看见白人图片或积极词汇按 “E” 键，亚裔图片或消极词汇按 “I” 键。如果被试判断错误，图片下方会出现一个红叉，提示被试修正自己的按键判断。在被试做出正确判断后，再进入下一个试次。

------

### 3  基于jsPsych的内隐联想测验实验程序编写教程

明确了实验设计，接下来本教程将教大家如何使用`jsPsych`一步步编写这个IAT实验。我们将使用 `jsPsych` 插件库来构建实验，其中涉及到被试信息收集、指导语编写、实验流程编写以及数据保存等内容。下面是具体的实现步骤和代码展示。

#### 3.1  引入相关插件

这个 HTML 页面结构设置了一个基础框架，用于运行基于 `jsPsych`  的 IAT 实验。使用CDN（内容分发网络）托管的脚本直接从互联网上加载`jsPsych` 库及相关插件以及相应的样式表，添加到`<head>` 部分中：

```javascript
<!DOCTYPE html>
<html>
<head>
    <title>IAT Experiment</title>
    <script src="https://unpkg.com/jspsych@7.3.4"></script>
    <script src="https://unpkg.com/@jspsych/plugin-html-keyboard-response@1.1.3">
    <script src="https://unpkg.com/@jspsych/plugin-preload@1.1.3"></script>
    <script src="https://unpkg.com/@jspsych/plugin-iat-html@1.1.3"></script>
    <link href="https://unpkg.com/jspsych@7.3.4/css/jspsych.css" rel="stylesheet" type="text/css" />
</head>
<body></body>
<html>
```

#### 3.2  弹性盒子的应用

运用CSS为实验页面提供清晰的布局和样式，使其适应屏幕以及不同类型的内容能够一致且有序地显示。将以下 CSS 添加到 `<style>` 部分中：

```javascript
<style>
    body {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
        font-family: Arial, sans-serif;
        background-color: #f0f0f0;
    }

    .flex-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100vh; 
        padding: 20px;
    }

    .image-container {
        max-width: 100%;
        max-height: 100vh;
        overflow: hidden;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .responsive-img {
        max-width: 25%;
        height: auto;
    }

    .words-container {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100%; 
    }

    .words-font {
        font-size: 3em; 
        line-height: 1.5; 
        text-align: center; 
        max-width: 100%;
    }
</style>
```

#### 3.3  初始化jsPsych

使用 `initJsPsych()` 初始化 `jsPsych`， 在实验结束时将数据保存为CSV文件并自动下载。

```javascript
<script>
    // 初始化jsPsych
    var jsPsych = initJsPsych({
        on_finish: function() {
        // 获取实验数据并将其转换为CSV格式
        var csvData = jsPsych.data.get().csv();
        // 创建一个Blob对象，包含CSV数据
        var blob = new Blob([csvData], { type: 'text/csv' });  
        // 创建一个下载链接并自动触发下载
        var link = document.createElement('a');  
        link.setAttribute('download', 'iat_experiment_data.csv');
        link.href = URL.createObjectURL(blob);
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
        // 显示数据
        jsPsych.data.displayData();
        }
    });
```

#### 3.4  创建时间线

创建一个时间线数组 `timeline`，用于存储实验的各个步骤。

```javascript
    // 创建时间线
    var timeline = [];
```

#### 3.5  预加载图片

预加载实验中需要使用的图像。

```javascript
    // 预加载图片
    var preload = {
        type: jsPsychPreload,
        images: [
            'img/asian1.jpg', 'img/asian2.jpg', 'img/asian3.jpg', 'img/asian4.jpg',
            'img/asian5.jpg', 'img/asian6.jpg', 'img/asian7.jpg', 'img/asian8.jpg',
            'img/white1.jpg', 'img/white2.jpg', 'img/white3.jpg', 'img/white4.jpg',
            'img/white5.jpg', 'img/white6.jpg', 'img/white7.jpg', 'img/white8.jpg',
        ]
        };
    timeline.push(preload);
```

#### 3.6  欢迎被试参与实验并收集被试信息

创建实验的欢迎界面，简单地显示欢迎信息和实验开始的提示。创建被试信息收集界面，显示一个表单，要求被试输入 ID、年龄和利手信息，点击提交按钮后数据被记录并自动进入正式实验。

```javascript
    // 欢迎参与实验
    var welcome = {
        type: jsPsychHtmlKeyboardResponse,
        stimulus: `
        <div class="flex-container">
        <h2> 欢迎参与实验！</h2>
        <h2> 请按任意键开始实验。</h2>
        </div>
        `,
        };
    timeline.push(welcome);

    // 收集被试信息
    var participant_info = {
        type: jsPsychHtmlKeyboardResponse,
        stimulus: `
            <div style="display: flex; justify-content: center; align-items: center; height: 100vh;">
            <div style="text-align: left; width: 300px;">
                <h2>被试基本信息收集：</h2>
                <form id="participant-info-form">
                    <label for="id">被试 ID: </label><input name="id" type="text" required><br><br>
                    <label for="age">年龄: </label><input name="age" type="number" required><br><br>
                    <label for="hand">利手（"0" : 左利手, "1" : 右利手）: </label><input name="hand" type="text" required><br><br>
                    <button type="button" id="submit-info">提交</button>
                </form>
                <p>请按【提交】继续实验。</p>
            </div>
        </div>
    `,
        choices: "NO_KEYS",
        on_load: function() {
            document.getElementById('submit-info').addEventListener('click', function() {
                var form = document.getElementById('participant-info-form');
                var formData = new FormData(form);
                var responses = {};
                formData.forEach(function(value, key) {
                    responses[key] = value;
                });

                // 将响应添加到 jsPsych 数据
                jsPsych.data.addProperties(responses);

                // 自动进行正式实验
                jsPsych.pluginAPI.cancelAllKeyboardResponses();
                jsPsych.finishTrial();
            });
        }
    };
    timeline.push(participant_info);
```

#### 3.7  总指导语

创建实验总指导语页面，使得被试了解实验任务。

```javascript
	//指导语
    var instructions = {
        type: jsPsychHtmlKeyboardResponse,
        stimulus: `
        <style>
            .left-align {
                text-align: left;
                display: inline-block;
            }
            .centered-content {
                text-align: center;
            } 
        </style>
        <div class="centered-content">
            <h3> 欢迎参加本次内隐联想测验(IAT)实验</h3>
            <p> 接下来的任务中, 将要求你对一组呈现的词语或图片进行分类。</p>
            <div class="left-align">
                <h3> 注意</h3>
                <p> · 请把双手食指放在'E'键和'I'键上以确保能尽快反应。</p>
                <p> · 左上角和右上角的两个标签将给予类别提示。</p>
                <p> · 如果您的判断发生错误, 刺激下方将会出现一个红叉, 请您及时修正判断。</p>
                <p> · 全程请保持注意力集中, 尽量快速且准确地做出判断。</p>
            </div>
            <p> 如果明白上述指导语, 请按任意键以继续实验!
        </div>
        `,
        post_trial_gap: 2000
    };
    timeline.push(instructions);
```

#### 3.8  定义图片和文字刺激

定义实验中所用到的刺激，包括图片和词汇两种。其中图片刺激集1用于阶段一和阶段三，图片刺激集2用于阶段四和阶段五；词汇刺激集用于阶段二、阶段三及阶段五。

```javascript
	// 定义图片刺激集1
    var images_stimuli_1 = [
        {stimulus: '<div class="image-container"><img src="img/asian1.jpg" class="responsive-img" alt="Asian Image 1"></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container"><img src="img/asian2.jpg" class="responsive-img" alt="Asian Image 2"></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container"><img src="img/asian3.jpg" class="responsive-img" alt="Asian Image 3"></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container"><img src="img/asian4.jpg" class="responsive-img" alt="Asian Image 4"></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container"><img src="img/asian5.jpg" class="responsive-img" alt="Asian Image 5"></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container"><img src="img/asian6.jpg" class="responsive-img" alt="Asian Image 6"></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container"><img src="img/asian7.jpg" class="responsive-img" alt="Asian Image 7"></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container"><img src="img/asian8.jpg" class="responsive-img" alt="Asian Image 8"></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container"><img src="img/white1.jpg" class="responsive-img" alt="White Image 1"></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container"><img src="img/white2.jpg" class="responsive-img" alt="White Image 2"></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container"><img src="img/white3.jpg" class="responsive-img" alt="White Image 3"></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container"><img src="img/white4.jpg" class="responsive-img" alt="White Image 4"></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container"><img src="img/white5.jpg" class="responsive-img" alt="White Image 5"></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container"><img src="img/white6.jpg" class="responsive-img" alt="White Image 6"></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container"><img src="img/white7.jpg" class="responsive-img" alt="White Image 7"></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container"><img src="img/white8.jpg" class="responsive-img" alt="White Image 8"></div>', stim_key_association: 'right'},
    ];

    // 定义图片刺激集2
    var images_stimuli_2 = [
        {stimulus: '<div class="image-container"><img src="img/asian1.jpg" class="responsive-img" alt="Asian Image 1"></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container"><img src="img/asian2.jpg" class="responsive-img" alt="Asian Image 2"></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container"><img src="img/asian3.jpg" class="responsive-img" alt="Asian Image 3"></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container"><img src="img/asian4.jpg" class="responsive-img" alt="Asian Image 4"></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container"><img src="img/asian5.jpg" class="responsive-img" alt="Asian Image 5"></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container"><img src="img/asian6.jpg" class="responsive-img" alt="Asian Image 6"></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container"><img src="img/asian7.jpg" class="responsive-img" alt="Asian Image 7"></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container"><img src="img/asian8.jpg" class="responsive-img" alt="Asian Image 8"></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container"><img src="img/white1.jpg" class="responsive-img" alt="White Image 1"></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container"><img src="img/white2.jpg" class="responsive-img" alt="White Image 2"></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container"><img src="img/white3.jpg" class="responsive-img" alt="White Image 3"></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container"><img src="img/white4.jpg" class="responsive-img" alt="White Image 4"></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container"><img src="img/white5.jpg" class="responsive-img" alt="White Image 5"></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container"><img src="img/white6.jpg" class="responsive-img" alt="White Image 6"></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container"><img src="img/white7.jpg" class="responsive-img" alt="White Image 7"></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container"><img src="img/white8.jpg" class="responsive-img" alt="White Image 7"></div>', stim_key_association: 'left'},
    ];

    // 定义词汇刺激集
    var words_stimuli = [
        {stimulus: '<div class="image-container words-container"><div class="responsive-img words-font">愉快</div></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container words-container"><div class="responsive-img words-font">和平</div></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container words-container"><div class="responsive-img words-font">美好</div></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container words-container"><div class="responsive-img words-font">善良</div></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container words-container"><div class="responsive-img words-font">光荣</div></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container words-container"><div class="responsive-img words-font">成功</div></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container words-container"><div class="responsive-img words-font">坚韧</div></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container words-container"><div class="responsive-img words-font">乐观</div></div>', stim_key_association: 'left'},
        {stimulus: '<div class="image-container words-container"><div class="responsive-img words-font">苦恼</div></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container words-container"><div class="responsive-img words-font">糟糕</div></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container words-container"><div class="responsive-img words-font">肮脏</div></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container words-container"><div class="responsive-img words-font">失败</div></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container words-container"><div class="responsive-img words-font">邪恶</div></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container words-container"><div class="responsive-img words-font">伤害</div></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container words-container"><div class="responsive-img words-font">悲观</div></div>', stim_key_association: 'right'},
        {stimulus: '<div class="image-container words-container"><div class="responsive-img words-font">沮丧</div></div>', stim_key_association: 'right'},
    ];
```

#### 3.9  IAT实验阶段一

实验的阶段一，包括该阶段的指导语和图片试次的流程。

```javascript
	// 阶段一：概念图片判断
    // 指导语
    var instructions_1 = {
        type: jsPsychHtmlKeyboardResponse,
        stimulus: `
            <div class="flex-container">
                <h2>现在进行概念图片判别任务。</h2>
                <p>所呈现图片是亚裔图片请按 "E" 键，白人图片请按 "I" 键。</p>
                <p>请尽可能快且准确地做出反应。</p>
                <h2>如果明白该指导语, 请按任意键继续。</h2>
            </div>
            `
        };
    timeline.push(instructions_1);

    // 图片trials
    var trial_images_1 = {
        type: jsPsychIatHtml,
        stimulus: jsPsych.timelineVariable('stimulus'),
        stim_key_association: jsPsych.timelineVariable('stim_key_association'),
        html_when_wrong: '<span style="color: red; font-size: 80px">X</span>',
        bottom_instructions: '<p>If you press the wrong key, a red X will appear. Press the other key to continue</p>',
        force_correct_key_press: true,
        display_feedback: true,
        trial_duration: 3000, // 仅当display_feedback为false的时候
        left_category_key: 'e',
        right_category_key: 'i',
        left_category_label: ['亚裔'],
        right_category_label: ['白人'],
        response_ends_trial: true,
    };

    // 将图片试次添加到时间轴并随机化顺序
    timeline.push({
        timeline: [trial_images_1],
        timeline_variables: images_stimuli_1,
        randomize_order: true
    });
```

#### 3.10  IAT实验阶段二

实验的阶段二，包括该阶段的指导语和词汇试次的流程。

```javascript
	// 阶段二：属性词汇判断
    // 指导语
    var instructions_2 = {
        type: jsPsychHtmlKeyboardResponse,
        stimulus: `
            <div class="flex-container">
                <h2>现在将进行词汇判别任务。</h2>
                <p>所呈现的词汇是积极词汇请按“E”, 消极词汇请按“I”。</p>
                <p>请尽可能快且准确地做出反应。</p>
                <h2>如果明白该指导语, 请按任意键继续。</h2>
            </div>
        `
    };
    timeline.push(instructions_2);

    // 词汇trials
    var trial_words = {
        type: jsPsychIatHtml,
        stimulus: jsPsych.timelineVariable('stimulus'),
        stim_key_association: jsPsych.timelineVariable('stim_key_association'),
        html_when_wrong: '<span style="color: red; font-size: 80px">X</span>',
        bottom_instructions: '<p>If you press the wrong key, a red X will appear. Press the other key to continue</p>',
        force_correct_key_press: true,
        display_feedback: true,
        trial_duration: 3000, // 仅当display_feedback为false的时候
        left_category_key: 'e',
        right_category_key: 'i',
        left_category_label: ['积极词汇'],
        right_category_label: ['消极词汇'],
        response_ends_trial: true
    };

    // 将试次添加到时间轴并随机化顺序
    timeline.push({
        timeline: [trial_words],
        timeline_variables: words_stimuli,
        randomize_order: true
    });
```

#### 3.11  IAT实验阶段三

实验的阶段三，包括该阶段的指导语以及图片和词汇试次的流程。

```javascript
	// 阶段三：概念图片和属性词汇判断
    // 指导语
    var instructions_3 = {
        type: jsPsychHtmlKeyboardResponse,
        stimulus: `
            <div class="flex-container">
            <h2>现在将进行词汇和图片判别任务。</h2>
            <p>看到亚裔图片或积极词汇请按 "E" 键。</p>
            <p>看到白人图片或消极词汇请按 "I" 键。</p>
            <p>请尽可能快且准确地做出反应。</p>
            <h2>如果明白该指导语, 请按任意键继续。</h2>
            </div>
        `
    };
    timeline.push(instructions_3);

     // 随机化图片和词汇刺激顺序
    images_stimuli = jsPsych.randomization.shuffle(images_stimuli_1);
    words_stimuli = jsPsych.randomization.shuffle(words_stimuli);

    // 混合刺激，交替图片和文字
    var combined_stimuli_1 = [];
        for (var i = 0; i < Math.max(images_stimuli.length, words_stimuli.length); i++) {
        if (i < images_stimuli.length) {
            combined_stimuli_1.push(images_stimuli[i]);
        }
        if (i < words_stimuli.length) {
            combined_stimuli_1.push(words_stimuli[i]);
        }
    }

    // 混合trial
    var combined_trial_1 = {
        type: jsPsychIatHtml,
        stimulus:jsPsych.timelineVariable('stimulus'),
        stim_key_association: jsPsych.timelineVariable('stim_key_association'),
        html_when_wrong: '<span style="color: red; font-size: 80px">X</span>',
        bottom_instructions: '<p>If you press the wrong key, a red X will appear. Press the other key to continue</p>',
        force_correct_key_press: true,
        display_feedback: true,
        trial_duration: 3000, // 仅当display_feedback为false的时候
        left_category_key: 'e',
        right_category_key: 'i',
        left_category_label: ['亚裔', '积极词汇'],
        right_category_label: ['白人', '消极词汇'],
        response_ends_trial: true
    };

    // 添加试次到时间轴
    timeline.push({
        timeline: [combined_trial_1],
        timeline_variables: combined_stimuli_1,
        randomize_order: false
    });
```

#### 3.12  IAT实验阶段四

实验的阶段四，包括该阶段的指导语和反向图片试次的流程。

```javascript
	// 阶段四：概念图片反向判断
    // 指导语
    var instructions_4 = {
        type: jsPsychHtmlKeyboardResponse,
        stimulus: `
            <div class="flex-container">
                <h2>现在进行图片判别任务，请注意按键有发生变化。</h2>
                <p>所呈现图示是白人请按 "E" 键，亚裔请按 "I" 键。</p>
                <p>请尽可能快且准确地做出反应。</p>
                <h2>如果明白该指导语, 请按任意键继续。</h2>
            </div>
        `
    };
    timeline.push(instructions_4);

    // 图片trial
    var trial_images_2 = {
        type: jsPsychIatHtml,
        stimulus: jsPsych.timelineVariable('stimulus'),
        stim_key_association: jsPsych.timelineVariable('stim_key_association'),
        html_when_wrong: '<span style="color: red; font-size: 80px">X</span>',
        bottom_instructions: '<p>If you press the wrong key, a red X will appear. Press the other key to continue</p>',
        force_correct_key_press: true,
        display_feedback: true,
        trial_duration: 3000, // 仅当display_feedback为false的时候
        left_category_key: 'e',
        right_category_key: 'i',
        left_category_label: ['白人'],
        right_category_label: ['亚裔'],
        response_ends_trial: true
    };

    // 将试次添加到时间轴并随机化顺序
    timeline.push({
        timeline: [trial_images_2],
        timeline_variables: images_stimuli_2,
        randomize_order: true
    });
```

#### 3.13  IAT实验阶段五

实验的阶段五，包括该阶段的指导语以及反向图片和词汇试次的流程。

```javascript
	// 阶段五：概念图片和属性词汇反向判断
    // 指导语
    var instructions_5 = {
        type: jsPsychHtmlKeyboardResponse,
        stimulus: `
            <div class="flex-container">
                <h2>现在将进行词汇和图片判别任务。</h2>
                <p>看到白人图片或积极词汇请按 "E" 键。</p>
                <p>看到亚裔图片或消极词汇请按 "I" 键。</p>
                <p>请尽可能快且准确地做出反应。</p>
                <h2>如果明白该指导语, 请按任意键继续。</h2>
            </div>
        `
        };
    timeline.push(instructions_5);

    // 随机化刺激顺序
    images_stimuli = jsPsych.randomization.shuffle(images_stimuli_2);
    words_stimuli = jsPsych.randomization.shuffle(words_stimuli);

    // 混合刺激，交替图片和文字
    var combined_stimuli_2 = [];
    for (var i = 0; i < Math.max(images_stimuli.length, words_stimuli.length); i++) {
    if (i < images_stimuli.length) {
        combined_stimuli_2.push(images_stimuli[i]);
    }
    if (i < words_stimuli.length) {
        combined_stimuli_2.push(words_stimuli[i]);
    }
    }

    // 图片和词汇trial
    var combined_trial_2 = {
        type: jsPsychIatHtml,
        stimulus: jsPsych.timelineVariable('stimulus'),
        stim_key_association: jsPsych.timelineVariable('stim_key_association'),
        html_when_wrong: '<span style="color: red; font-size: 80px">X</span>',
        bottom_instructions: '<p>If you press the wrong key, a red X will appear. Press the other key to continue</p>',
        force_correct_key_press: true,
        display_feedback: true,
        trial_duration: 3000, // 仅当display_feedback为false的时候
        left_category_key: 'e',
        right_category_key: 'i',
        left_category_label: ['白人', '积极词汇'],
        right_category_label: ['亚裔', '消极词汇'],
        response_ends_trial: true
    };

    // 添加试次到时间轴
    timeline.push({
        timeline: [combined_trial_2],
        timeline_variables: combined_stimuli_2,
        randomize_order: false
    });

```

#### 3.14  结束语

创建结束语页面，告知被试实验结束并表达感谢。

```javascript
	// 结束语
    var end = {
        type: jsPsychHtmlKeyboardResponse,
        stimulus: `
        <div class="flex-container">
            <h2>实验结束，谢谢参与！</h2>
            <h2>按任意键退出实验。</h2>
        </div>
        `
    };
    timeline.push(end);
```

#### 3.15  启动实验

最后，启动实验。

```javascript
	// 开始实验
    jsPsych.run(timeline);

</script>
```

------

### 4  运行实验

将上述代码保存为 `.html` 文件，然后在浏览器中打开即可开始实验。在运行之前，请明确图片路径并更换成自己的路径。

------

### 5  结果查看

实验结束后，生成的数据文件将自动下载到您的计算机中。数据文件包括被试的基本信息和每次实验的详细数据（例如，反应时、正确率等）。

------

### 6  Flexbox布局分析

本实验的 HTML 文件中，使用了 Flexbox 布局来管理页面元素。下面是对 Flexbox 布局部分的详细分析。

#### 6.1  整体布局

```javascript

body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
}
```

> - **`display: flex;`**: 将整个网页的布局方式设置为 Flexbox，这是一种用于创建灵活且高效布局的布局模型。
> - **`justify-content: center;`**: 将内容水平居中。
> - **`align-items: center;`**: 将内容垂直居中。
> - **`height: 100vh;`**: 设置页面的高度为视口高度的 100%，确保内容在页面上垂直居中。
> - **`margin: 0;`**: 移除默认的页面外边距。
> - **`font-family: Arial, sans-serif;`**: 设置字体族为 Arial 或其他 sans-serif 字体。
> - **`background-color: #f0f0f0;`**: 设置背景颜色为浅灰色。
>

------

#### 6.2  容器布局

```javascript
.flex-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh; /* Full viewport height */
    padding: 20px;
}
```

> - **`display: flex;`**: 将容器设置为 Flexbox 布局。
> - **`flex-direction: column;`**: 使子元素按列排列。
> - **`align-items: center;`**: 将子元素水平居中。
> - **`justify-content: center;`**: 将子元素垂直居中。
> - **`height: 100vh;`**: 容器高度设置为视口高度的 100%。
> - **`padding: 20px;`**: 添加 20 像素的内边距。
>

------

#### 6.3  图片刺激容器布局

```javascript
.image-container {
    max-width: 100%;
    max-height: 100vh;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
}

.responsive-img {
    max-width: 25%;
    height: auto;
}
```

> - **`max-width: 100%;`**: 限制图像容器的最大宽度为其父容器的 100%。
>
> - **`max-height: 100vh;`**: 限制图像容器的最大高度为视口高度的 100%。
>
> - **`overflow: hidden;`**: 超出容器的内容会被隐藏。
>
> - **`display: flex;`**: 使用 Flexbox 布局。
>
> - **`justify-content: center;`**: 将子元素水平居中。
>
> - **`align-items: center;`**: 将子元素垂直居中。
>
> - **`max-width: 25%;`**: 图像的最大宽度设置为父容器宽度的 25%，确保图像不超出其容器。
>
> - **`height: auto;`**: 根据宽度自动调整高度，保持图像的原始宽高比。
>

------

#### 6.4  词汇刺激容器布局

```javascript
.words-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%; /* Ensures the container takes the full height available */
}

.words-font {
    font-size: 3em; /* Adjust the font size as needed */
    line-height: 1.5; /* Line height for proper spacing */
    text-align: center; /* Center text within the words container */
    max-width: 100%;
}
```

> - **`display: flex;`**: 使用 Flexbox 布局。
>
> - **`justify-content: center;`**: 将文本内容水平居中。
>
> - **`align-items: center;`**: 将文本内容垂直居中。
>
> - **`height: 100%;`**: 容器的高度为其父容器的 100%。
>
>   
>
> - **`font-size: 3em;`**: 设置字体大小为 3 倍于默认字体大小。
>
> - **`line-height: 1.5;`**: 设置行高为 1.5，增加行间距。
>
> - **`text-align: center;`**: 将文本居中对齐。
>
> - **`max-width: 100%;`**: 文本的最大宽度为其父容器的 100%，防止超出容器。
>

------



综上，通过这些精心设计的布局和样式，确保网页内容在不同设备和屏幕尺寸上都能良好地显示，提供更好的视觉效果和用户体验。
