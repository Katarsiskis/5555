# 5555
 По умолчанию (без аргументов) git log перечисляет коммиты, сделанные в репозитории в обратном к хронологическому порядке — последние коммиты находятся вверху. Из примера можно увидеть, что данная команда перечисляет коммиты с их SHA-1 контрольными суммами, именем и электронной почтой автора, датой создания и сообщением коммита.

Команда git log имеет очень большое количество опций для поиска коммитов по разным критериям. Рассмотрим наиболее популярные из них.

Одним из самых полезных аргументов является -p или --patch, который показывает разницу (выводит патч), внесенную в каждый коммит. Так же вы можете ограничить количество записей в выводе команды; используйте параметр -2 для вывода только двух записей:

NAME
git-log - Show commit logs

SYNOPSIS
git log [<options>] [<revision-range>] [[--] <path>…​]
DESCRIPTION
Shows the commit logs.

List commits that are reachable by following the parent links from the given commit(s), but exclude commits that are reachable from the one(s) given with a ^ in front of them. The output is given in reverse chronological order by default.

You can think of this as a set operation. Commits reachable from any of the commits given on the command line form a set, and then commits reachable from any of the ones given with ^ in front are subtracted from that set. The remaining commits are what comes out in the command’s output. Various other options and paths parameters can be used to further limit the result.

Thus, the following command:

$ git log foo bar ^baz
means "list all the commits which are reachable from foo or bar, but not from baz".

A special notation "<commit1>..<commit2>" can be used as a short-hand for "^<commit1> <commit2>". For example, either of the following may be used interchangeably:

$ git log origin..HEAD
$ git log HEAD ^origin
Another special notation is "<commit1>…​<commit2>" which is useful for merges. The resulting set of commits is the symmetric difference between the two operands. The following two commands are equivalent:

$ git log A B --not $(git merge-base --all A B)
$ git log A...B
The command takes options applicable to the git-rev-list[1] command to control what is shown and how, and options applicable to the git-diff[1] command to control how the changes each commit introduces are shown.