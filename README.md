# Multi-level Side Menu

Ionic 2 demo of a two-level side menu. The component currently supports only two levels of items. 

If more levels are needed, maybe using tabs layout for the other levels would be a better approach.

## Running the demo

Inside of the project folder, run `npm install` and then to run the demo in the browser `ionic serve [-t android/ios]`

### Using the component in your projects

Just copy the `side-menu` folder (inculding the html, ts and scss files) in your project. Then include it in the `declarations` array from your `@NgModule`.

Menu and sub menu items should have the following format:

```
// Base Interface
export interface MenuOptionModel {
	iconName: string;
	displayName: string;
	component: any;
	isLogin: boolean;
	isLogout: boolean;
	subItems?: Array<MenuOptionModel>;
}
```

So an item with nested sub items would look like this:

```
let menuOption: MenuOptionModel = {
    iconName: 'ios-arrow-down',
    displayName: `Option Name`,
    component: PageName,
    isLogin: false,
    isLogout: false,
    subItems: [
        {
            iconName: 'ios-basket',
            displayName: `Sub Option 1`,
            component: PageName,
            isLogin: false,
            isLogout: false
        },
        {
            iconName: 'ios-bookmark',
            displayName: `Sub Option 2`,
            component: PageName,
            isLogin: false,
            isLogout: false
        }
    ]
};
```

When an option is selected, the `MenuOptionModel` object is returned to the caller, so it can check which option was selected and if the user should be redirected to a given page, or the login / logout logic should be executed.

The component support two modes: default and accordion. To enable the accordion mode just add `[accordionMode]="true"` to the `side-menu-content` element.

```
<side-menu-content [accordionMode]="true" [options]="options" (selectOption)="selectOption($event)"></side-menu-content>
```

The component also exposes the `collapseAllOptions()` method to reset the state of the options when needed (when closing the menu for instance).
