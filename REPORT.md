
## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
```
https://github.com/Dm1tryb1t/lab002
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
git push origin main
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
git push origin main
```
9. Проверьте, что история коммитов доступна в удалёный репозитории.
```sh
git log
```
Результат:
```
commit 0142029dcfec36ecfb39d0ba2c04c68adac978de (HEAD -> main, origin/main)
Author: Dm1tryb1t <afanasevdima465@gmail.com>
Date:   Thu May 30 10:58:44 2024 +0300

    red

commit a3bd1dcea42f10d4b4614b158f0d0f09ad18793d
Author: Dm1tryb1t <afanasevdima465@gmail.com>
Date:   Thu May 30 10:44:32 2024 +0300

    add hellowrld

commit e365f8163f040ed1af66190919605689311f3673
Author: Dm1try <144801808+Dm1tryb1t@users.noreply.github.com>
Date:   Thu May 30 10:49:58 2024 +0300

    Update Hello_world.cpp

commit 5a51fbc362d7a775185e8488a6cd3a60eff683a7
Merge: 3cb4aac ddf9241
Author: Dm1try <144801808+Dm1tryb1t@users.noreply.github.com>
Date:   Thu May 30 10:48:55 2024 +0300


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
git push origin patch1
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
git push origin patch2
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
Copyright (c) 2015-2024 The ISC Authors
```
