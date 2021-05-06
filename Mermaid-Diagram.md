[Original issue, please commment there if Mermaid is useful](https://github.com/wekan/wekan/issues/3794)

## Npm package

- NPM package at https://www.npmjs.com/package/@liradb2000/markdown-it-mermaid

## About examples

- Below examples and more at https://mermaid-js.github.io/mermaid/#/examples

## Howto

- Add mermaid code to Wekan card or any other input field. After some time, if chart is not visible, reload browser webpage.
- Mermaid code starts with `~~~mermaid`
- Mermaid code ends with `~~~`

## Example 1: Flowchart

```
~~~mermaid
    graph TD
    A[Client] --> B[Load Balancer]
    B --> C[Server01]
    B --> D[Server02]
~~~
```

## Example 2: Pie Chart

```
~~~mermaid
pie title NETFLIX
         "Time spent looking for movie" : 90
         "Time spent watching it" : 10
~~~
```

## Example 3: Gantt Chart

```
~~~mermaid
gantt
    dateFormat  YYYY-MM-DD
    title       Adding GANTT diagram functionality to mermaid
    excludes    weekends
    %% (`excludes` accepts specific dates in YYYY-MM-DD format, days of the week ("sunday") or "weekends", but not the word "weekdays".)

    section A section
    Completed task            :done,    des1, 2014-01-06,2014-01-08
    Active task               :active,  des2, 2014-01-09, 3d
    Future task               :         des3, after des2, 5d
    Future task2              :         des4, after des3, 5d

    section Critical tasks
    Completed task in the critical line :crit, done, 2014-01-06,24h
    Implement parser and jison          :crit, done, after des1, 2d
    Create tests for parser             :crit, active, 3d
    Future task in critical line        :crit, 5d
    Create tests for renderer           :2d
    Add to mermaid                      :1d

    section Documentation
    Describe gantt syntax               :active, a1, after des1, 3d
    Add gantt diagram to demo page      :after a1  , 20h
    Add another diagram to demo page    :doc1, after a1  , 48h

    section Last section
    Describe gantt syntax               :after doc1, 3d
    Add gantt diagram to demo page      :20h
    Add another diagram to demo page    :48h
~~~
```