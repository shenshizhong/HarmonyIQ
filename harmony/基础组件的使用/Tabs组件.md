
Tabs 组件
```
一般用在底部，或者顶部导航栏。(就是菜单栏)

Tab(value:{barPosition?: BarPosition, index?: number, controller?: TabsController})

barPosition 设置Tabs 的页签位置 (显示在哪里，比如显示在底部)
index 设置初始页签索引
controller 设置Tabs 控制器，用于控制Tabs 组件进行页签的切换

Tabs是组件属性
vertical 设置Tabs是否为纵向
barMode TabBar 布局模式
barWidth TabBar的宽度

使用：
Tab({barPosition: BarPosition.Start}){
    ...
}
.vertical(false)
.barWidth('100%')
.barHeight(60)

tabBar 属性介绍
tarBar(value: string| Resource|CustomBuilder|{icon?: string|Resource; text?:string|Resource;})

private controller: TabsController = new TabsController()

Tabs({barPosition: BarPosition.Start, controller: this.controller}){
  TabContent(){
  }
  .tabBar('green')
        
  TabContent(){
  }
  .tabBar('blue')      
} 

使用@Builder,构建自定义TabBar。实现tab菜单
struct MainPage{
    @State currentIndex: number = 0
    private tabsController: TabsController = new TabsController();
    
    @Builder TabBuilder(title: string, index: number,
                        selectedImg: Resource, normalImg: Resource){
        Column(){
            Image(this.currentIndex === index ? selectedImg : normalImg)
            Text(title)
                .fontColor(this.currentIndex === index ? '#1698CE' : '#6B6B6B')
        }
    }
    .onClick(()=>{
        this.currentIndex = index;
        this.tabsController.changeIndex(index);
    })
    
    build(){...}
    
}  

```

构建一个主页面
```
struct MainPage{
    @State currentIndex: number = 0;
    private tabsController: TabsController = new TabsController();
    @Builder TabBuilder(...){...}

    build(){
        Tab({barPosition: BarPosition.End, controller: this.tabsController}){
            TabContent(){
                Home()
            }
            .tabBar(this.TabBuilder('首页', 0, $r(app.media.home_selected),
            $r('app.media.home_normal')))
            
            TabContent(){
                Setting()
            }
            .tabBar(this.TabBuilder('我的', 1, $r(app.media.mine_selected),
            $r('app.media.mine_normal')))
        }
        .barWidth('100%')
        .barHeight(56)
        .barMode(BarMode.Fixed)
        .onChange((index: number) => {
            this.currentIndex = index;
        })
    }
}

```