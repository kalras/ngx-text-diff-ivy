# ngx-text-diff
- A simple text diff `component` to be used with Angular and based on `google diff match patch` library.

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 17.0.8.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The application will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via a platform of your choice. To use this command, you need to first add a package that implements end-to-end testing capabilities.

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.io/cli) page.


## Demo
[Ngx Text Diff Demo](https://ngx-text-diff.herokuapp.com/home)

## Installation
`npm i ngx-text-diff`

## API
`module: NgxTextDiffModule`  
`component: NgxTextDiffComponent`  
`selector: td-ngx-text-diff`

### Inputs
| Input                | Type              | Required                        | Description                                                                                     |
| -------------------- | ----------------- | ------------------------------- | ----------------------------------------------------------------------------------------------- |
| left                 | string            | Yes                             | First text to be compared                                                                       |
| right                | string            | Yes                             | Second text to be compared                                                                      |
| diffContent          | Observable        | Optional                        | `DiffContent` observable                                                                        |
| format               | `DiffTableFormat` | Optional, default: `SideBySide` | Possible values:<br> -`SideBySide`<br> -`LineByLine`                                            |
| loading              | boolean           | Optional, default: `false`      | Possible values:<br> -`true`: shows an loading spinner.<br>- `false`: hides the loading spinner |
| hideMatchingLines    | boolean           | Optional, default: `false`      | Possible values:<br> -`true`: Only shows lines with differences.<br>- `false`: shows all lines  |
| showToolbar          | boolean           | Optional, default: `true`       | Possible values:<br> -`true`: shows the toolbar.<br>- `false`: hides the format toolbar         |
| showBtnToolbar       | boolean           | Optional, default: `true`       | Possible values:<br> -`true`: shows the format toolbar.<br>- `false`: hides the format toolbar  |
| outerContainerClass  | any               | Optional                        | `ngClass` object for the outer div                                                              |
| outerContainerStyle  | any               | Optional                        | `ngStyle` object for the outer style                                                            |
| toolbarClass         | any               | Optional                        | `ngClass` object for the toolbar div                                                            |
| toolbarStyle         | any               | Optional                        | `ngStyle` object for the toolbar style                                                          |
| compareRowsClass     | any               | Optional                        | `ngClass` object for the div surrounding the table rows                                         |
| compareRowsStyle     | any               | Optional                        | `ngStyle` object for the div surrounding the table rows                                         |
| synchronizeScrolling | boolean           | Optional, default: `true`       | Possible values:<br> -`true`: Scrolls both tables together.<br>- `false`: Scrolls individually  |

### Output
| Input          | Type        | Required | Description                             |
| -------------- | ----------- | -------- | --------------------------------------- |
| compareResults | DiffResults | Optional | Event fired when comparison is executed |

### Custom Objects
``` typescript
export interface DiffContent {
  leftContent: string;
  rightContent: string;
}

export type DiffTableFormat = 'SideBySide' | 'LineByLine';

export interface DiffResults {
  hasDiff: boolean;
  diffsCount: number;
  rowsWithDiff: {
    leftLineNumber?: number;
    rightLineNumber?: number;
    numDiffs: number;
  }[];
}
```

## Usage
1. Register the `NgxTextDiffModule` in a module, for example app module.
``` typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { ScrollDispatchModule } from '@angular/cdk/scrolling';

import { AppComponent } from './app.component';
import { NgxTextDiffModule } from 'ngx-text-diff';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, ScrollDispatchModule, NgxTextDiffModule],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

``` typescript
import { Component, OnInit } from '@angular/core';
import { DiffContent, DiffResults } from 'ngx-text-diff/lib/ngx-text-diff.model';

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: []
})
export class HomeComponent implements OnInit {
  left = `some text to\nbe compared!`
  right = `A changed\n version \n of the text to\nbe compared!`

  constructor() {}

  ngOnInit() {
  }

  onCompareResults(diffResults: DiffResults) {
    console.log('diffResults', diffResults);
  }
}

```

``` html
<td-ngx-text-diff
  [left]="left"
  [right]="right"
  (compareResults)="onCompareResults($event)"
>
```

## Build the NgxTextDiff module

Run `ng build ngx-text-diff` to build the library. The build artifacts will be stored in the `dist/ngx-text-diff` directory.

## Credits

This project is based on [google diff match patch](https://github.com/google/diff-match-patch).
