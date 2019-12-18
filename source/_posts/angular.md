---
title: Angular
date: 2018-11-15 17:00:23
categories: 
- DevNote
- Angular
tags: 
- 金魚腦
---
---
<!--more-->
## 指令
- `ng new [name]`：建立一個全新的angular app
- `ng serve`：會啟動一個開發server。 網址為`http://localhost:4200/` ，程式會自動reload當修改程式的時候。
    -  目前專案使用 `npm run start` 來啟用 `ng serve`
    -  `--open`：serve會自動開啟開發網頁
    -  `--port portnumber(default 4200)`：修改預設port
- `ng nuild`：
    - 目前專案使用 `npm run build`來建立deploy的程式
    - `--prod`
    - `--prod --output-hashing=none`
    - `--aot`
- `ng generate`/`ng g`：新增 `component|directive|pipe|service|class|guard|interface|enum|module`
  ex: `ng g component componentname` :componentname 可為path/componentname

## 路由
- 路由設定在`app-routing.module.ts`。angular的設定會由上而下，所以如果設定兩個同樣的path，會以最下面的路由來做載入。
    {% codeblock lang:typescript %} 
        const routes: Routes = [
            //A.預設若路由為空，則導入根目錄
            { path: '', redirectTo: '/', pathMatch: 'full' }, 
            //B.路由導入到NameComponent
            { path: 'name', component: NameComponent },
            //C.LazyLoading 需指定對應module
            { path: 'name', loadChildren: './Name/Name.module#NameModule'} 
        ];
    {% endcodeblock %}
- B.路由導入到componenet
  - 建立component指令：`ng generate component [name]`，會產生下列檔案：
    - `name.component.ts`
    - `name.component.html`
    - `name.component.css`
    - `name.component.spec.ts`
  - `app.module.ts`中加入declarations`Namecomponent`
    {% codeblock lang:typescript %} 
        import { NameComponent } from './Name/Name.component';
        
        @NgModule({
        declarations: [
            NameComponent,
        ],
        })
    {% endcodeblock %}
  - `app-routing.module.ts`
     {% codeblock lang:typescript %} 
    import { NameComponent } from './Name/Name.component';

    const routes: Routes = [
      { path: 'name', component: NameComponent },
    ];
        {% endcodeblock %}
- C.Lazy Loading：這個需要先行建立component對應的module及routing。
  - 建立對應module及routing指令：`ng generate module [name] --routing`，會產生下列檔案：
    - `name-routing.module.ts`
    - `name.module.ts`
    - `name.module.spec.ts`
  - `app-routing.module.ts`
     {% codeblock lang:typescript %} 
    const routes: Routes = [
      { path: 'name', loadChildren: './name/name.module#NameModule'}
    ];
        {% endcodeblock %}
  - `name.module.ts`：設定載入的module、component etc.
     {% codeblock lang:typescript %} 
    import { NameRoutingModule } from './name-routing.module';
    import { NameComponent } from './name.component'; 

    @NgModule({
      imports: [
        CommonModule,
        NameRoutingModule,
      ],
      declarations: [
        NameComponent
      ],
      providers: []
    })
        {% endcodeblock %}
  - `name-routing.module.ts`：設定自己的routing
     {% codeblock lang:typescript %} 
    import { NameComponent } from './name.component';
    const routes: Routes = [
      //目前這個資料夾中，沒有別的component，所以就這樣指定就好
      { path: '', component: NameComponent }, 
      // 如果還有別的compoent，就是加上去
      // { path: 'n1', component: N1Component }
    ];
    {% endcodeblock %}