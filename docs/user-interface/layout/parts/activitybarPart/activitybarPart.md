# ActivitybarPart 


```ts
// vs/workbench/browser/parts/activitybar/activitybarPart.ts

export class ActivitybarPart extends Part implements IActivityBarService {
	// 获取到注册到 activitybarPart 的视图
	private getViewContainers(): readonly ViewContainer[] {
		return this.viewDescriptorService.getViewContainersByLocation(this.location);
	}

	override createContentArea(parent: HTMLElement): HTMLElement {

		// View Containers action bar
		this.compositeBarContainer = this.compositeBar.create(this.content);

	}
}

// vs/workbench/browser/parts/compositeBar.ts
export class CompositeBar extends Widget implements ICompositeBar {
	create(parent: HTMLElement): HTMLElement {
		this.compositeSwitcherBar = this._register(new ActionBar(actionBarDiv, {
			actionViewItemProvider: action => {
				return item && this.instantiationService.createInstance(CompositeActionViewItem);
			}
		}));
	}
}

// vs/workbench/browser/parts/compositeBarActions.ts
export class CompositeActionViewItem extends ActivityActionViewItem {

}
```
