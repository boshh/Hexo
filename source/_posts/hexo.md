---
title: Hexo
date: 2018-11-14 14:31:34
categories: 
- DevNote
tags:
- 金魚腦
---
---
<!--more-->

### 指令
- 寫作 https://hexo.io/zh-tw/docs/writing
    - `hexo new [post(文章) default,page,draft(草稿)] <title>`
- Deploy https://hexo.io/zh-tw/docs/commands
    - `hexo deploy -g`

### 標籤
- 繼續閱讀 `<!--more-->`
  
### 格式
- 日期 
    - YYYY-MM-DD 2018-11-14
    - YY-MMM 2018-11月
    - YY-MMMM 2018-November
- 區塊
    - blockquote
        {% blockquote %} blockquote{% endblockquote %}
    - codeblock
        {% codeblock lang:typescript %} 		
        @Output() onHideSRW: EventEmitter<any> = new EventEmitter();

        onHide(){
            this.onHideSRW.emit(false);
        } 
        {% endcodeblock %}


