
## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
```
https://github.com/COTOPESq/lab002
```
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
```sh
cat > Hello_world.cpp <<EOF
#include <iostream>

using namespace std;

int main(){
cout << "Hello world" << endl;
}

EOF
```
4. Добавьте этот файл в локальную копию репозитория.
5. Закоммитьте изменения с *осмысленным* сообщением.
```sh
git add .
git push --set-upstream origin main
```
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
```sh
cat > Hello_world.cpp <<EOF
#include <iostream>
#include <string> 

using namespace std;

int main(){
string name;
cout << "enter name: " << endl;
cin >> name;
cout << "Hello world " << name << endl;
}

EOF
```
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
```sh
git add .
git commit -m"add..."
```
8. Запуште изменения в удалёный репозиторий.
```sh
git push --set-upstream origin main
```
9. Проверьте, что история коммитов доступна в удалёный репозитории.
```sh
git log
```
Результат:
```
commit 950b1ade84844eccc12fabf92d9fa1d825b11f57 (HEAD -> main, origin/main)
Author: COTOPESq <slava20082005@gmail.com>
Date:   Sat Apr 13 10:08:17 2024 +0300

    Add @name_user enter

commit 58c898b6cbb15de90aac3def2cf9c71e033e5abc
Author: COTOPESq <slava20082005@gmail.com>
Date:   Sat Apr 13 10:01:05 2024 +0300

    add Hellow_world.cpp

commit ee73d3b7586c458efa2520bf659b7616e9da69c6
Author: COTOPESq <slava20082005@gmail.com>
Date:   Fri Apr 12 13:25:06 2024 +0300

    added README.md and .gitignore

```

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
```sh
git branch patch1
```
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
```sh
cat > Hello_world.cpp <<EOF
#include <iostream>
#include <string> 

int main(){
string name;
std::cout << "enter name: " << std::endl;
std::cin >> name;
std::cout << "Hello world " << name << std::endl;
}

EOF
```
3. **commit**, **push** локальную ветку в удалённый репозиторий.
```sh
git add .
git commit -m"add..."
git push --set-upstream origin patch1
```
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
```
Доступна
```
5. Создайте pull-request `patch1 -> master`.
```
pull-request обработал
```
6. В локальной копии
 в ветке `patch1` добавьте в исходный код комментарии.
```sh
 cat > Hello_world.cpp <<EOF
#include <iostream>
#include <string> 

int main(){
string name;
std::cout << "enter name: " << std::endl; //show text
std::cin >> name; //enter name
std::cout << "Hello world " << name << std::endl; //result
}

EOF
```
7. **commit**, **push**.
```
Повторение пунктов с комитами
```
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
10. Локально выполните **pull**.
```sh
git pull origin
```
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
```sh
git log
```
12. Удалите локальную ветку `patch1`.
```sh
git branch -d patch1
```

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
```sh
git checkout -b patch2
```
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
```sh
clang-format -i -style=Mozilla "Hello world.cpp"
```
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
```sh
git add .
git commit -m"add..."
git push --set-upstream origin patch2
```
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
```
#include <iostream>
#include <string> //text

int main(){
string name;
std::cout << "enter name: " << std::endl; //show text.
std::cin >> name; //enter name.
std::cout << "Hello world " << name << std::endl; //result.
}
```
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
```sh
git pull origin main
git rebase main
edit "Hello_world.cpp"
git add .
git commit -m"..."
git rebase --continue
```
7. Сделайте *force push* в ветку `patch2`
```sh
git push -f origin patch2
```
8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2021 The ISC Authors
```
