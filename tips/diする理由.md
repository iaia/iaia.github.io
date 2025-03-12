diする理由

インスタンス化の詳細を知らなくて済む

例えば
GetUserNameUseCase と UserRepository があるとする

GetUserNameUseCaseがUserRepositoryからgetNameする
UserRepositoryはDatabaseインスタンスから getUserName をする

のようなとき

diをしない場合

GetUserNameUseCase {
repository = UserRepository(Database())
repository.getName()
}

みたいに、UseCaseが、RepositoryにはDatabaseが必要で、おそらくそこからデータを取るのだということが知られてしまう
つまり詳細を知ってしまうことになる

更に、データベースではなく、ネットワークAPIから取得する、ということになった場合に

repository = UserRepository(NetworkAPI())

みたいな変更をしなければならない。
Repositoryだけの関心事である「どこからデータを取るか?」ということをユースケースも知る必要があることになる。

diをする場合

GetUserNameUseCase(
repository: UserRepository
) {
repository.getName()
}

こうなる
つまり、repositoryがどこからともなくデータを取ってくる
さらにユースケースがその裏にある存在を知らなくて済む

外部に詳細が漏れない

外部に詳細が漏れないということは、それだけ変更が最小限になるということ

