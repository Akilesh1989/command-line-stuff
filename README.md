## List of commands I found useful

1. List all files modified in a commit:
    ```
    git diff-tree --no-commit-id --name-only -r <COMMIT_HASH>
    ```

2. Setup git credentials locally.

    To setup your git credentials locally and to avoid having to provide your username and password everytime you pull and push, run
    ```
    git config credential.helper store
    ```
    then do a git pull and provide your username and password

3. Get specific line numbers from a file:
    ```
    sed -n '207,208p;370,400p' <FILENAME>
    ```
    This will return lines `207`, `208` and lines `369` through `400`

4. Split a comma delimited file and find the unique counts for each value in a given column
    If `input.csv` is
    ```
    fruit, qty
    apple, 1
    banana, 2
    carrot, 3
    apple, 4
    ```
    and we want to find the count of fruits, then run
    ```
    cat input.csv | awk '{split($0, a, ","); print a[1]}' | sort | uniq -c
    ```
    The output will be,
    ```
    2 apple
    1 banana
    1 carrot
    1 fruit
    ```

5. `awk` with an `if` condition
    If `input.csv` is
    ```
    fruit, qty
    apple, 1
    banana, 2
    carrot, 3
    apple, 4
    ```
    and we want to find out which of these fruits have a count more than 1, then
    ```
    cat input.csv | awk '{split($0, a, ","); print a[1]}' | sort | uniq -c | awk '{ if ($1 > 1) print $2":"$1}'
    ```
    The output will be,
    ```
    apple:2
    ```

6. Loop through files in a directory to search for a keyword
    ```
    find . -iname "*" -type f | xargs grep "<KEYWORD>"
    ```

    Alternatively you can use [the_silver_searcher](https://github.com/ggreer/the_silver_searcher).
