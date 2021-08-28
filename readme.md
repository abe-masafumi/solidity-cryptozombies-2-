# Solidity
<img src="home.png">

- データベースのゾンビをオーナーに与える
> この作業には新しいデータ型が必要になる。 mapping と addressだ。  

- アドレス
> イーサリアムのブロックチェーンが銀行口座と同じようにアカウント（口座）で構成されている  
> （口座）には、Ether（イーサ）の残高が記録されていて、Ether（イーサリアムブロックチェーンで使用される通貨）を送金したり受け取ったり、別のアカウントに支払うこともできるのだ。銀行口座から送金するのと全く同じだと思っていい  
> それぞれのアカウントにはアドレスがある  
> 例:  
> `0x0cE446255506E92DF41614C46F1d6df9Cc969183`  

----------------------------------------------------------
# Mappings（マッピング）
> mappingとは、Solidityで使用する配列のような機能です  
```sol
// 金融系のアプリの場合、ユーザーのアカウントの残高にuintを格納する：
mapping (address => uint) public accountBalance;
// もしくは、ユーザーIdを基にユーザー名を参照・格納するために使用するぞ：
mapping (uint => string) userIdToName;
```
> マッピングは本質的にはデータの保管と参照のためのキーバリューストアだ。最初の例で言えば、キーはaddress で、バリュー（値）はuintだ。２番目の例だと、キーは uint で、バリューは stringだ。  

- アクセス修飾子
* public
> publicで指定された場合は、指定した場所（内部）からも、指定していない場所（外部）からもアクセス可能です。  
* private
> privateで指定した場合は、そのcontractからのみアクセス可能です。  
* external
> externalで指定した場合は、指定していない場所（外部）からのみアクセス可能です。  
* internal
> internalで指定した場合は、そのcontractと、そのcontractの子からアクセス可能です。  

- Array と Mapping はけっこう違います。
> 他の言語の Mapping と同じと解説してあるところもありますが、そうだと思って開発を進めるとハマります。  
> 特に、Ethereum 本番環境で、Gas を使う必要があるトランザクションの場合にはコスト面において大きな違いになります。マイナー(採掘者)は、Gas Priceが低いトランザクションを無視する自由があり、通常のマイナーは、Gas Priceが高いものから実行していきます。そのため、Gas を適切に消費する戦略が Ethereum アプリを開発する上で必要になります。  
----------------------------------------------------------
- msg.sender
> 全ての関数で利用できるグローバル変数の一つ。これを使用すると、その関数を呼び出したユーザー（またはスマートコントラクト）の addressを参照できる  

- require
> requireはある条件を満たさない場合はエラーを投げて実行を止めることができる  
```sol
function sayHiToVitalik(string _name) public returns (string) {
  // まず_nameが"Vitalik"と同じかどうか比較する。真でなければエラーを吐いて終了させる。
  // （注：Solidityはネイティブで文字列比較ができない。そこで文字列の比較を
  // するためにkeccak256 を使ってハッシュ同士を比較する方法を使うのだ。
  require(keccak256(_name) == keccak256("Vitalik"));
  // もし真ならば、関数を処理する：
  return "Hi!";
}
```

- クラスの継承 
> 別ファイルで引き継げる  
> import　と　isだけ  
> 例：  
```sol
import "./someothercontract.sol";

contract newContract is SomeOtherContract {

}
```

- storage とmemory
> Storage はブロックチェーン上に永久に格納される変数  
> Memoryは一時的な変数で、外部関数をコントラクトに呼び出す際に消去されるもの  

