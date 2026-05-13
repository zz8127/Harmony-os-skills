# UI 设计组件库（UI Design Kit）

> HarmonyOS 6.1 / API 23

## 概述

UI 设计组件库（UI Design Kit）提供符合 HarmonyOS 设计规范的高阶 UI 组件，通过 `@kit.UIDesignKit` 引入。包含导航、标签页、列表项、侧边栏、操作栏、提示条和材质效果等组件，API 23 新增多项增强特性。

## HdsNavigation

高阶导航组件，支持分栏模式、分割线、占位符、标题大小和材质效果。

```typescript
import { HdsNavigation } from '@kit.UIDesignKit';

@Entry
@Component
struct NavigationPage {
  build() {
    Column() {
      HdsNavigation({
        title: '页面标题',
        subtitle: '副标题',
        navigationType: HdsNavigation.NavigationType.NORMAL,
        showDivider: true,
        titleSize: HdsNavigation.TitleSize.LARGE,
        materialEnabled: true
      })
    }
  }
}
```

分栏模式导航：

```typescript
import { HdsNavigation } from '@kit.UIDesignKit';

@Entry
@Component
struct SplitNavigationPage {
  build() {
    Column() {
      HdsNavigation({
        title: '分栏导航',
        navigationType: HdsNavigation.NavigationType.SPLIT,
        showDivider: true,
        showPlaceholder: true,
        materialEnabled: true
      })
    }
  }
}
```

## HdsTabs

高阶标签页组件，支持浮动样式、迷你标签栏和材质效果。

```typescript
import { HdsTabs } from '@kit.UIDesignKit';

@Entry
@Component
struct TabsPage {
  build() {
    Column() {
      HdsTabs({
        tabs: [
          { title: '首页', icon: $r('app.media.tab_home') },
          { title: '发现', icon: $r('app.media.tab_discover') },
          { title: '我的', icon: $r('app.media.tab_mine') }
        ],
        tabStyle: HdsTabs.TabStyle.FLOATING,
        onTabClick: (index: number) => {
          console.info(`选中: ${index}`);
        }
      })
    }
  }
}
```

迷你标签栏（API 23 材质效果）：

```typescript
import { HdsTabs } from '@kit.UIDesignKit';

@Entry
@Component
struct MiniBarTabsPage {
  build() {
    Column() {
      HdsTabs({
        tabs: [
          { title: '推荐' },
          { title: '热门' },
          { title: '最新' }
        ],
        tabStyle: HdsTabs.TabStyle.MINI_BAR,
        materialEnabled: true,
        onTabClick: (index: number) => {
          console.info(`选中: ${index}`);
        }
      })
    }
  }
}
```

## HdsListItem / HdsListItemCard

高阶列表项组件，支持无障碍、菜单样式和滑动删除。

```typescript
import { HdsListItem, HdsListItemCard } from '@kit.UIDesignKit';

@Entry
@Component
struct ListPage {
  build() {
    Column() {
      List() {
        ListItem() {
          HdsListItem({
            title: '设置项',
            subtitle: '描述信息',
            icon: $r('app.media.ic_setting'),
            accessoryType: HdsListItem.AccessoryType.ARROW,
            accessibilityText: '打开设置',
            onItemClick: () => {
              console.info('点击设置项');
            }
          })
        }

        ListItem() {
          HdsListItemCard({
            title: '卡片标题',
            description: '卡片描述内容',
            image: $r('app.media.card_image'),
            menuStyle: HdsListItemCard.MenuStyle.DROPDOWN,
            onMenuClick: (menuId: string) => {
              console.info(`菜单: ${menuId}`);
            }
          })
        }
      }
    }
  }
}
```

滑动删除（API 23）：

```typescript
import { HdsListItem } from '@kit.UIDesignKit';

@Entry
@Component
struct SwipeDeletePage {
  build() {
    Column() {
      List() {
        ListItem() {
          HdsListItem({
            title: '可滑动删除项',
            subtitle: '左滑删除',
            swipeAction: {
              enableSwipeDelete: true,
              onDelete: () => {
                console.info('执行删除');
              }
            }
          })
        }
      }
    }
  }
}
```

## HdsSidebar

高阶侧边栏组件，API 23 新增滑动手势开关支持。

```typescript
import { HdsSidebar } from '@kit.UIDesignKit';

@Entry
@Component
struct SidebarPage {
  build() {
    HdsSidebar({
      sidebarContent: () => {
        this.SideMenuContent();
      },
      mainContent: () => {
        this.MainContent();
      },
      enableSwipeGesture: true,
      onSidebarShow: () => {
        console.info('侧边栏打开');
      },
      onSidebarHide: () => {
        console.info('侧边栏关闭');
      }
    })
  }

  @Builder
  SideMenuContent() {
    Column() {
      Text('菜单项 1')
      Text('菜单项 2')
      Text('菜单项 3')
    }
  }

  @Builder
  MainContent() {
    Column() {
      Text('主内容区域')
    }
  }
}
```

## HdsActionBar

高阶操作栏组件，API 23 新增边距设置。

```typescript
import { HdsActionBar } from '@kit.UIDesignKit';

@Entry
@Component
struct ActionBarPage {
  build() {
    Column() {
      Text('页面内容')

      HdsActionBar({
        actions: [
          { title: '收藏', icon: $r('app.media.ic_fav') },
          { title: '分享', icon: $r('app.media.ic_share') }
        ],
        mainAction: { title: '立即购买' },
        marginSettings: {
          startMargin: 16,
          endMargin: 16,
          topMargin: 8,
          bottomMargin: 8
        },
        onMainActionClick: () => {
          console.info('点击主操作');
        }
      })
    }
  }
}
```

## HdsSnackbar

高阶提示条组件，API 23 新增自动高度适配。

```typescript
import { HdsSnackbar } from '@kit.UIDesignKit';

function showSnackbar(): void {
  HdsSnackbar.show({
    message: '操作成功',
    duration: HdsSnackbar.Duration.SHORT,
    autoHeight: true,
    action: {
      text: '撤销',
      onClick: () => {
        console.info('撤销操作');
      }
    }
  });
}
```

## HdsMaterial

材质效果组件，API 23 支持设置材质类型和层级。

```typescript
import { HdsMaterial } from '@kit.UIDesignKit';

@Entry
@Component
struct MaterialPage {
  build() {
    Column() {
      HdsMaterial({
        materialType: HdsMaterial.MaterialType.BLUR,
        materialLevel: HdsMaterial.MaterialLevel.LEVEL_2,
        cornerRadius: 16
      }) {
        Text('材质效果内容')
          .fontSize(16)
          .fontColor(Color.White)
      }
      .width(300)
      .height(100)
    }
  }
}
```

## 权限

| 权限 | 说明 |
|------|------|
| 无特殊权限 | UI 组件库无需额外权限 |

## 官方参考

- [UI Design Kit 开发指南](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ui-design-kit-overview-0000001820880929)
- [UI Design Kit API 参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/hds-navigation-0000001774121278)
