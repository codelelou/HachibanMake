# 概要
8番ライクをプログラミング不要で作れるゲームのテンプレートです。  
「8番ライク」は「[8番出口](https://store.steampowered.com/app/2653790/8/?l=japanese)」（『異変を見つけたら引き返す、見つからなかったら引き返さない』というルールの異変探しゲーム）の影響を強く受けたゲームを指します。

このゲームのテンプレートでは、何かが消えたり現れたり、何かの位置が変わったり、何かが大きくなったりするような表示・位置・角度・大きさが変化する異変だけであればプログラミングができなくても8番ライクゲームを作ることができます。  

開発の手順は「レベル作成」「異変リスト作成」「異変設定」の3ステップ。  

まずはシティシム感覚で、異変探しの舞台となるレベル（地形や建物）をダウンロードした3Dモデルなどを配置して作成します。  
レベル作成が終わればゲームの大半が完成したようなもので、後は異変リストを作成し、レベルに配置したオブジェクトに異変を設定するだけです。  

## 異変探しゲーム以外も作れる
異変探しゲームしか作れないように思うかもしれませんが、内部処理的には「異変」に縛られる必要はありません。  
フラグが立っているかどうか（異変があるか）に過ぎません。  

コイントス（異変の有無の抽選）を行い、プレイヤーはその表裏を回答（引き返すか引き返さないか）しているようなものです。  
そしてコインが表の時（異変がある時）はリストからIDを抽選し、そのIDを元に表示を切り替えます（画面上に異変を起こす）。  

例えば、このロジックで「ウォーリーをさがせ！」的なゲームも作れます。  
コインが表の時にウォーリーが現れ、ウォーリーを見つけたら進む、見つけられなかったら引き返すみたいな。  

アイデア次第で異変探しゲーム以外も作れるので、是非、異変探し以外のゲーム開発にも挑戦してみてください。  

# 導入（開発環境構築）
このゲームのテンプレートはゲームエンジンのUnreal Engineのプロジェクトファイルのため、Unreal Engineをインストールする必要があります。  

## Unreal Engineのバージョン
Unreal Engine 5.4  

このバージョン以降のもであれば動作する可能性は高いですが、Unreal Engineのアップデートによる仕様変更で正常に動作しなくなることはあります。  
その場合はこのゲームのテンプレートの対応バージョンのUnreal Engineをインストールしてください（1つの端末に異なる複数のバージョンのUnreal Engineのインストールは可能です）。  

なお、このゲームのテンプレートのアップデート時に対応するUnreal Engineのバージョンが変更になることはあります。  

## Unreal Engineのインストール
インストールについてはUnreal Engine全般のテーマのため、詳しくは[Unreal Engineダウンロードページ](https://www.unrealengine.com/ja/download)や解説動画などを参考にしてください。  

「Unreal Engine インストール」や「Unreal Engine 入門」などのキーワードで探してみてください。  
このゲームのテンプレートを編集する前に、入門者向け・初心者向けの動画などでイメージを掴んだり、Unreal Engineそのものに慣れておくのも良いと思います。  

## ゲームのテンプレートをダウンロードする
GitHubページ上の緑色の［Code］ボタンを左クリックし、表示されるメニューの［Download ZIP］ボタンを左クリックします。  
そして案内に従ってそのZIPファイルを端末に保存します。  

ダウンロードが完了したらそのZIPファイルをわかりやすい場所に展開（解凍）します。  
ゲーム開発ではSSDなどの高速ストレージに展開することを推奨します。  

またディレクトリ構造が深いとゲームエンジンの不具合に繋がることがあるため、浅いディレクトリ階層に展開してください（例えば「D:\UnrealProjects\HachibanMake」など）。  
あわせて親フォルダも含めてフォルダ名は半角英数字のみで構成するようにしてください（Unreal Engineに限らずゲーム開発ではフォルダ名・ファイル名に日本語があると不具合の原因になることがあります）。  

そして展開したUnreal EngineプロジェクトファイルであるHachibanMake.uproject（ファイル名は変更可能ですが、Unreal Engineの仕様により20文字以内が良いそうです）をダブルクリックすれば、対応するUnreal Engineが起動し編集できるようになると思います。  
もし直接開けない場合は、次で説明するUnreal Engineを起動してからプロジェクトファイルを指定して開く方法を試してください。  

## Unreal Engineを起動する
起動するとプロジェクトブラウザが開くと思うので、左上の［最近使用したプロジェクト］を左クリックし、右下の［ブラウズ］ボタンを左クリックしてください（以前からUnreal Engineを使っている場合は自動的に最近開いていたプロジェクトが自動ロードされてしまっている場合があるので、その場合はそれを閉じてプロジェクトブラウザを開いてください）。  

そして先程ダウンロードして展開したゲームのテンプレートのアンリアルプロジェクトファイル「HachibanMake.uproject」を開いてください。  
これでこのゲームのテンプレートを編集できるようになると思います。  

# 8番ライクゲームの作り方
開発の手順は大きく「レベル作成」「異変リスト作成」「異変設定」の3ステップ。  

レベル作成でゲームの大部分が完成し、レベル作成はシティシムで地形や建物を作るようなイメージです。  
はじめは既存のサンプルレベルを装飾する感じで3Dモデルを配置するだけにして、Unreal Engineに慣れることを目標にしても良いと思います。  

レベル作成が終わったら異変リストを作成し、その異変をレベル上のオブジェクトに設定していくだけです。  
ゲームの進行や異変の抽選、メニュー表示などはプログラミング済みです。  

## 異変探しゲームのルール設定
初期設定は8番出口にルールに合わせているので特に変更しなくても問題はありませんが、設定値を書き換えることで変更可能です。  
Hcbn_BP_AnomalyMasterブループリント（/Hachiban/Anomaly/Hcbn_BP_AnomalyMaster.uasset）を開き、画面中央上部のデフォルトボタンを左クリックし、右側の詳細タブの［設定］にある項目をお好みで変更してください。  

![Hcbn_BP_AnomalyMasterブループリントの設定変数の場所](https://github.com/user-attachments/assets/0237d652-0d92-4f42-bd2d-c2b6874991a3)

* AnomalyDataTable…異変リストデータテーブルファイル。
* LastRound…クリア条件基準となるラウンド数（何番出口か）。
* MustSafeLastRoundEndCondition…LastRoundに異変がない時をクリア条件に含めるか（100%異変発生モードではこの設定は無効）。
* AnomalyProbability…基本異変発生率。
* ZeroRoundAnomalyProbability…0ラウンドの異変発生率
* LastRoundAnomalyProbability…最終ラウンドの異変発生率（MustSafeEndRound=True時は高め推奨）
* DifficultTag…異変リストでこのタグを持つ異変は終盤に優先的に発生（8番出口では終盤に即死系異変が発生しやすいらしい）。
* PermissileNoAnomalies…連続異変無し許容回数（8番出口では3回らしい）。
* Mode…失敗時0に戻る／失敗時1つ前まで戻る／異変発生率100％。

## 【ステップ1】 レベル作成（地形や建物などのマップ作成）
Hcbn_Level_Topレベルファイル（/Hachiban/Level/Hcbn_Level_Top）を開き、サンプルレベルを編集（装飾・改造）する感じでレベルを作成します。
デフォルト設定のままならエディタ起動時にこのレベルファイルが開くと思います。  

なおUnreal Engineでのゲーム開発において「レベル」はゲームの舞台となる地形や建物などステージとなる「マップ」を指し、経験値や難易度の意味ではありません。  
またレベル上に配置する3Dモデルや光源、オーディオファイルなどは「アクター」と呼びます（プログラムファイルであるブループリントに「アクター」クラスが名称が混在してややこしいですが注意してください）。  

### まずはサンプルゲームをプレイしよう
動作確認を兼ねて、エディタ上でサンプルゲームをプレイしてみましょう（開発中の動作確認やテストプレイでよく使うことになる基本操作でもあります）。  
そもそもサンプルゲームが動かなければ、これから作るゲームも動かないでしょう。  

エディタ上部中央あたりに表示されるプレイボタン（再生ボタン）か、その横の縦3つ点ボタンから「選択ビューポート」か「新規エディタウィンドウ（PIE）」を左クリックします。  
サンプルゲームはキーボード・マウスだけでなく、Xboxコントローラーが接続されて入ればゲームパッドでのプレイも可能です（PlayStationやSwitchのコントローラーなどはWindowsに標準対応ではないのためそのままでは使えません）。  

![レベルプレイボタンの位置の図解](https://github.com/user-attachments/assets/829b765b-6f03-4b50-a8aa-e30ca947dd1e)

問題がなければ普通にサンプルゲームをクリアまで、さらにはクリア後の異変回収もできます。  
このプレイモードはEscキーで終了します。

ゲーム内のメニュー表示はゲームパッドのオプションボタンかPキーで開きます（本来はEscキーでも開きますが、エディタ側の設定によりプレイモード自体が終了してしまいます）。  
なおプレイモードが「スタンドアローンゲーム」の時はEscキーでは終了しません（この場合はゲーム内メニューの終了ボタンから終了できます）。  

また言語変更もプレイモード「スタンドアローンゲーム」でないと正常に動作しません（これ以外のプレイモードで言語を変更するとエディタの表示言語が切り替わる恐れがあります）。  

#### クリア後のゲーム開始位置
クリア後はゲーム開始位置が未確認の異変の案内の前からはじまるようになります。  

初回起動時と同じ場所からプレイする場合は確認した異変のデータをリセットする必要があります。  
ゲーム内メニューの［異変一覧］ボタンから異変一覧を開き、右上のリセットボタンからリセットできます。  

なおクリア後のゲーム開始位置は変更可能ですが、フラグ管理に影響があり位置が悪いとバグの原因となるため、もしクリア後のゲームプレイに支障が出るような場合はクリア後のゲーム開始位置の切替自体を諦める判断も必要です（これで不具合が発生した場合、修正は上級者向けとなります）。  

### レベル作成の注意点（制約）
レベル上にはプレイヤーがどのように移動しているを把握するための見えない当たり判定（フラグ管理するトリガー）があります。  
このトリガーによって回答（異変を見つけた・見つからなかった）の受付や、進行方向のステージの事前読込などを行っています。  

レベルの構造によってはこれらのトリガーを避けて通れるようになる恐れがあり、それにより正常に回答を受け付けられなかったり、進行先のステージが読み込まれなかったりといったバグ発生が考えられます。  
このゲームのテンプレートに慣れるまでは、これらのトリガーの移動・拡大縮小は避け、可能な限りサンプルの通路（床・壁）に沿ってオブジェクト配置するようにしてください。  

### レベル本体の編集
Hcbn_Level_Topレベルファイルはサンプルゲームの大本となるレベルですが、ループ表示されるステージ本体はHcbn_Level_MainStageレベルファイルになります。  

Hcbn_Level_Topレベル上にHcbn_Level_MainStageレベルを読み込み、ゲーム進行に応じて複数のHcbn_Level_MainStageレベルを表示することでループを実現しています。  
これにより本家「8番出口」のように暗転や画面切替を経由しないループができ、異変を見逃した時に直前のマップに戻って見逃した異変を探すこともできます。  
そのためHcbn_Level_Topレベル上に直接配置したオブジェクトはループ処理には使われないので注意してください。  

そしてHcbn_Level_Topレベル上のHcbn_Level_MainStageレベルはそのままではロック状態（編集不可）のため、まずはそれを解除（編集可能）する必要があります。  
Hcbn_Level_Topレベル上でHcbn_Level_MainStageレベルを選択状態にして、右クリックして表示されるメニューから［レベル > 編集］を左クリックし、編集可能状態にします。  

![レベルインスタンスの編集不可解除の図解](https://github.com/user-attachments/assets/4265ec7e-b763-4be9-aa73-362670de1ff6)

編集後は保存し、画面下部中央に表示されている［Hcbn_Level_MainStage 終了］の［終了］ボタンを左クリックします。  

![レベルインスタンス編集終了ボタンの位置の図解](https://github.com/user-attachments/assets/8d05b8d6-edff-4269-b764-0a804d56640e)

#### サンプルのオブジェクトを移動・複製・削除してみよう  
まずは練習として、Hcbn_Level_MainStageレベル上のアルファベットのA～Hのどれかを移動・複製・削除してみてください。  
これらのアルファベットは異変に使用していないため、サンプルゲームの異変には影響ありません。  

編集したいオブジェクトを選択すると3方向矢印（XYZ軸）が表示されると思います（3方向矢印以外の時はキーボードのWキーで操作の種類を移動に切り替えてください）。  
移動したい方向の矢印をドラッグして移動できます。  
Altキーを押しながら移動させると複製されたものが移動します。  
移動させずにDeleteキーを押せば削除できます。  

![操作モード切替ボタンの位置の図解](https://github.com/user-attachments/assets/f8b8cdac-9f93-4c08-82ba-2af78914263b)

他のオブジェクトを編集しても良いですが、床や壁を消してしまうとプレイヤーの落下に繋がったりそもそも道を進めなくなる恐れがあります。  
また異変として使っているオブジェクト（例えば乱雑に貼られた禁煙ポスターなど）を消そうとすると、参照されているオブジェクトとしてメッセージが表示されると思うので、その時はキャンセルし誤って削除しないように注意してください。消してしまうと異変が発生しても対象となるオブジェクトがないために正常に異変を発生させることができなくなります。  

![参照中のオブジェクトを消そうとする時に表示されるメッセージ](https://github.com/user-attachments/assets/dee6fff8-acbd-4f37-8e7e-1339f024d5e8)

移動・複製・削除を行ったら、エディタ上でプレイし、ループしても毎回同じようにその編集が反映されているかを確認します。  

#### オブジェクトを追加してみよう
エディタ上部左側にある立方体に緑のプラス記号付いたボタンを左クリックして表示されるメニュー内の［形状］から［キューブ］をレベル上に配置してみましょう。  

![キューブ追加ボタンの位置の図解](https://github.com/user-attachments/assets/4d404ab7-bb26-4c73-a93b-84f4561e1c71)

配置できたら、エディタ上でプレイしてループでも同じように表示されるかを確認します。  
もしループ時に表示されない場合は誤ってHcbn_Level_Topレベル上に配置してしまった可能性があります。その時はそのオブジェクトを削除し再配置してください。  

#### 進行状況の表示
本家「8番出口」の「何番出口」かの進行状況表示はHcbn_BP_Actor_Anomaly_Round_TextRenderアクター（/Hachiban/Anomaly/Actor/Round/Hcbn_BP_Actor_Anomaly_Round_TextRender.uasset）で行っています。  

![配置しているHcbn_BP_Actor_Anomaly_Round_TextRenderの図解](https://github.com/user-attachments/assets/b4cf7aff-b36f-45d8-bf36-da15dbe36376)

サンプルでは参考として、進行状況に応じて棒も近くに表示させてもいます（Hcbn_BP_Actor_Anomaly_Round_TextRenderアクターのCountActors変数）。  
これは作成するレベルの世界観やテーマによっては直接数字を表示をするのは合わないような時を想定したサンプルになります。  
例えば蝋燭が増えることで進行状況がわかるようになるといった表現が可能になります。  

またHcbn_BP_Actor_Anomaly_Round_TextRenderアクターのNumberActors変数では数字別のアクターを設定することも可能です。  
例えば全ての数字の画像をアクターとして配置し、それをNumberActorsに設定して使用します。  

ただ細部にまで拘りすぎると慣れるまでは時間がかかりすぎるため、はじめは割り切ってシンプルに数字を表示するだけでも良いと思います。  

#### ゴールの作り方
ゴールにはHcbn_BP_Actor_Anomaly_Goalアクター（/Hachiban/Anomaly/Actor/Goal/Hcbn_BP_Actor_Anomaly_Goal.uasset）を使います。  
サンプルの「Goal!」と表示されたオブジェクトを参考にしてください（「Goal!」の文字はレベル作成時のみ表示され、プレイ中はゴールする時であっても表示されません）。  

![配置しているHcbn_BP_Actor_Anomaly_Goalの図解](https://github.com/user-attachments/assets/a491b4da-fbfc-41e0-9c92-a28d233597c2)

最低限必要なのはゴールした判定を取得するトリガーで、レベル内で選択し、詳細タブの［デフォルト > Triggers］に要素を追加してレベル上のトリガー用のアクターを選択する必要があります。  
サンプルではGoalTriggerアクターになります。  

ただトリガーだけではプレイヤーには視覚的にゴールであることが認識できないため、ShowActors（Show＝見せる）とHideActors（Hide＝隠す）で視覚的にゴールを作ります。  
サンプルではゴール可能時に表示するアクターと非表示にするアクターを設定しており、ゴール時は曲道にせず壁と床を追加して直線にして階段代わりの上り坂を表示しています（ShowActorsに設定）。  
そして不要な壁とラウンド数表示などをHideActorsに設定しています。  

レベル作成に慣れるまでは1つのレベル上に通常のルートとゴール用のルートを混在させるのは難しいでしょうから、ゴール用のトリガーを大きくして設置し、その中央あたりにゴールっぽいオブジェクトを配置するだけでも良いかもしれません。  

なおゴール時に表示されるUIはHcbn_WBP_Endingユーザーウィジット（Hachiban/Anomaly/Actor/Goal/Hcbn_WBP_Ending.uasset）になります。  
これをカスタマイズすることでクリア時のUIを変更することが可能です。  

#### 【重要】Hcbn_BP_LevelHelper_MainStageアクター
Hcbn_BP_LevelHelper_MainStageアクター（/Hachiban/Blueprint/LevelHelper/Hcbn_BP_LevelHelper_MainStage.uasset）はプレイヤーがどこを通過したかを監視して、異変探しゲームを運用しているとても重要なアクターです。  

![配置したHcbn_BP_LevelHelper_MainStageの図解](https://github.com/user-attachments/assets/b1e0caf5-a26c-41bb-aa17-82538c696adb)

下手に弄るとバグの発生につながりやすいので、わからないで編集することがないように注意してください。  
進行先のレベル生成や回答（異変の有無）などが正常に行われなくなる恐れがあります。  

##### 入口と出口の場所
Hcbn_BP_LevelHelper_MainStageアクターのFrontStageTransform変数とBackStageTransform変数で、レベルの入口と出口の起点となる場所を設定しています。  

動的に進行先にレベルを生成してループを実現している関係上、入口と出口の位置は非常に重要です。  
ここがズレるとループ時に道がズレて表示されますし、ズレが大きいと視覚的に不自然になるだけでなく先に進めなくなる恐れもあります。  

慣れるまではサンプルの床と壁を装飾する感じ（オブジェクトで覆い隠す）にし、位置は動かさない方が失敗しにくいです。  

入口の起点はBackStageTransformNoteアクターで、引き返す際にここを起点に同じレベルが生成されて表示されます。  
入口の位置はXYZの座標がすべてゼロ（回転のZ軸が180なのは、引き返す時は道を逆側に生成するため）とわかりやすいので、基本的にレベルの寸法を変更する場合は出口側を移動させてください。  

![配置しているBackStageTransformNoteの図解](https://github.com/user-attachments/assets/7c139661-75c7-4f55-8e2b-fd7059efb69f)

出口の起点はFrontStageTransformNoteアクターです。  

![配置しているFrontStageTransformNoteの図解](https://github.com/user-attachments/assets/6f6fd794-23b7-400d-adbc-3e5ba68c8828)

##### 3種類のトリガー（フラグ）管理
Hcbn_BP_LevelHelper_MainStageアクターでは重要なトリガー（フラグ）を管理しており、ここをプレイヤーが通過すると自動的に処理を実行します。  
これらはのトリガーはレベルの出入口にあり、各3つの計6つのトリガーを設定しています。  

![3種類のトリガーの配置位置の図解](https://github.com/user-attachments/assets/dbdd7860-048c-4c0d-b1ae-51ab4c30bbb5)

+ Entryトリガー（レベルに入ったことを管理し、異変発生時はこれに触れた時にレベルに異変が現れる）
* Answerトリガー（引き返したか引き返さなかったかを、プレイヤーがこれに触れた時に判断）
* Stageトリガー（プレイヤーがこれに触れた時に、その先のレベルを生成してループを実現する）

つまりこれらを変に弄ると異変が現れなかったり、回答が受け付けられなかったり、進んだ先に道が無かったりとバグの原因になります。  

##### 異変がある時に引き返さすのか引き返させないのか

* FrontAnswerToIsAnomaly変数（初期値=Falseで異変がない時は引き返さない）
* BackAnswerToIsAnomaly変数（初期値=Trueで異変がある時は引き返す）

![Hcbn_BP_LevelHelper_MainStageの異変がある時に引き返すかどうかの切替設定の図解](https://github.com/user-attachments/assets/c60edf8f-7ab6-4635-9254-ce33f35a6f09)

この2つの変数で異変があった時に引き返すのか引き返さないのかの設定が可能です。  

上級者向けになりますが、両方とも異変無し回答としてFalseに設定し、異変を写真に取った時に正しければ追加プログラム内で異変有りとして回答させるといったようなことも可能ではあります。  

##### その他の管理
重要なトリガー管理の他に、補助的に2つのものを管理しています。  
これら2つは無くてもゲームの進行には影響しません。  

*SalvageTriggers変数（想定外のルートを通りプレイヤーが落下した時などにリスポーンさせるためのトリガー）
*UncheckedAnomalyGuidePlayerTransform変数（クリア後に残りの異変の案内板の前にスポーンさせたい時のスポーン先の設定）

![SalvageTriggers用トリガーの配置位置の図解](https://github.com/user-attachments/assets/db424ada-e853-4c9e-b5f9-230914bda352)

UncheckedAnomalyGuidePlayerTransform変数はスポーン場所によっては想定外のフラグが発生することありバグの原因になることがあるので、クリア後の異変回収の挙動に問題が発生するような時はクリア後のスポーン先変更を諦める判断も重要です。  
基本的にはEntryトリガーの内側にする必要があります。そうしないと進行先にレベルが読み込まれずループできないバグの原因になり、それを回避するのはプログラムの追加が必要になります（上級者向け）。  

![UncheckedAnomalyGuidePlayerTransform変数用のアクターの図解](https://github.com/user-attachments/assets/cd14e501-6fd1-4b70-80da-74fe98f6c626)

#### Hcbn_Level_Topレベル
これまでは主にループに使用するHcbn_Level_MainStageレベル上の話でしたが、このゲームの大本となるトップレベルであるHcbn_Level_Topレベル（/Hachiban/Level/Hcbn_Level_Top.umap）について説明します。  
ここでは重要なものが3つあります。  

* Hcbn_BP_LevelHelper_Topアクター（トップレベルであるHcbn_Level_Topレベルを管理するアクター）
* ループするレベルのインスタンス（サンプルではHcbn_Level_MainStageレベル）
* PlayerStart（起動時にプレイヤーがスポーンされる場所）

![Hcbn_Level_Topの図解](https://github.com/user-attachments/assets/19d8add1-384e-4452-9a21-c394763cb228)

レベル上のHcbn_BP_LevelHelper_Topアクター（/Hachiban/Blueprint/LevelHelper/Hcbn_BP_LevelHelper_Top.uasset）のStartLevelInstance変数にはループするレベルのインスタンスであるレベル上のHcbn_Level_MainStageレベルインスタンスを設定しています。  
これにより新たに生成された別レベルに入った時に不要になったループ用のレベルとして非表示になります。  

PlayerStartはサンプルを参考にEntryトリガーの間になるようにしてください。  
なぜなら一度Entryトリガーにプレイヤーが触れないとループ先となる前後の別レベルに移動する時に道が生成されないからです（具体的にはEntryトリガーに触れないとStageトリガーが動作しない）。  

##### BGMの設定
サンプルゲームは環境音すらなく無音のため、可能であれば環境音やBGMを追加しましょう。  

まずはフリー音源サイトなどから入手したサウンドファイルをわかりやすいフォルダにインポートしておきます（Wav形式などの一部の音楽フォーマットにしか対応していません）。  
そしてレベル上のHcbn_BP_LevelHelper_Topアクターを選択し、詳細タブの［デフォルト > Sound］にそのインポートしたファイルを設定しましょう。  

![Hcbn_BP_LevelHelper_TopへのSoundファイルの設定個所の図解](https://github.com/user-attachments/assets/0fd8cbb7-0b3e-4b39-926d-86f258d81946)

ここで使用する音源はループ設定しておいてください。  
エディタ上で開き、詳細タブの［サウンド > Looping］を有効（チェックを入れる）にします。  

![サウンドウェーブのループ設定個所の図解](https://github.com/user-attachments/assets/426ceb35-9b15-4e95-acbf-355f7c5942fe)

なおループ感覚の調整を行うには、そのサウンドファイルをサウンドキューやMetaSoundとして設定すれば可能ですが、ここでの説明は割愛します。  
Unreal Engineに慣れるまではインポートするサウンドファイルの後ろに無音を挿入してループの間隔を調整する方が簡単と思います。  

#### レベルを完成させよう
レベル編集の基本がわかれば、後はシティシム感覚でレベル作っていくだけです。  

先程オブジェクトを追加する時に開いたメニュー内の［Quixel Bridge］からプロ仕様の3Dオブジェクトを追加しても良いでしょう（Unreal Engineのライセンスに含まれているので無料で使えますが、ハイクオリティ故に使いすぎるとゲームサイズが増えるだけでなくゲームのパフォーマンスにも影響しかねないので注意してください）。  
もしくはUnrealマーケットプレイスからアセットを入手しても良いでしょう（このマーケットプレイスからダウンロードできるアセットには無料のものも含めゲーム素材として使ってよいライセンスが付与されています）。  
または[RealityScan](https://www.unrealengine.com/ja/realityscan)でスマホのカメラなどでスキャンしたものを3Dモデルとして取り込んでも良いでしょう（フリーゲームとして公開するつもりであっても漫画の違法コピーと同様にフィギュアなどの使用には著作権上の問題があるので注意してください）。  

![QuixelBridgeを開くメニューの位置の図解](https://github.com/user-attachments/assets/d08f7668-e68a-4753-8509-d82c6d89308d)

使用する3Dモデルによっては当たり判定がなくプレイヤーが通り抜けてしまうものがありますが、このような場合はコリジョンの設定を変更してみてください。

まずはシティシム感覚で地形作り・建物建築を楽しんで、異変探しゲームは忘れて自分が作るレベルを散歩してみても良いでしょう。  
最悪サンプルゲームが正常に動作しなくなっても、サンプルを新たにインストールしなおせば良いので、失敗から学ぶつもりで恐れず色々と挑戦してみましょう。  

なおサンプルゲームで異変として使われているオブジェクトは、削除しようとしても参照されているオブジェクトとしてメッセージが出ると思いますが、この時は削除をキャンセルしてください。  
ステップ3の異変設定の時の参考になるでしょうから、邪魔にならない場所に移動させておいてください。  

それとゲーム開発を一通り経験して全体を理解することも大切なので、はじめはあまりレベル作成に拘らずに次のステップに進んでも良いと思います。  

##### サウンドを配置するには
BGMではなく配置するオブジェクトが発する音も、3Dモデルなどと同様にサウンドファイルを配置することができます。  
さらに異変として設定すれば、異変によって音が再生したり停止したりします。  

ただし、ただ配置しただけではプレイヤーキャラクターの位置に関係なく聞こえてしまうので、減衰設定を行います（立体音響となり音の位置とプレイヤーキャラクターの位置に応じて音量も変化する）。  

まず配置した音声ファイルを選択し、その詳細タブの［アテニュエーション > OverrideAttenuation］を有効（チェックを入れる）にします。  
これを有効にすると［減衰（ボリューム）］が表示されるようになるので、[公式ドキュメントのサウンドの減衰](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/sound-attenuation-in-unreal-engine)などを参考に、［減衰関数］［減衰最短距離］［フォールオフ距離］などを調整します。  
わからなければ［減衰関数］を「Natural Sound」（自然な減衰処理）にし、［減衰最短距離］と［フォールオフ距離］をそれぞれ「400」前後にすると良いでしょう。特にフォールオフ距離の初期値が大きく、ループ先でも音が聞こえてしまう恐れがあります。  

![レベル上のオーディオファイルの減衰設定個所の図解](https://github.com/user-attachments/assets/d3b956c4-2d77-4c10-b8ad-fb0550c26cde)

なお減衰設定はサウンドオブジェクト毎に個別に設定せず、ファイル化して減衰設定を共通化できもしますが、ここでは割愛しています。  

また配置するサウンドファイルはBGMと同様にループ設定を有効にした方が良いでしょう。  

#### 異変作りについて
プログラミングせずに作る場合、発生した異変のIDを元にオブジェクトの表示非表示を切り替えるだけになります。  

オブジェクトが大きくなる異変の場合は、通常のオブジェクトを複製し、複製したオブジェクトのサイズを大きくし、通常サイズと大きなサイズの両方を配置する形になります。そして異変IDに非表示用オブジェクトとして通常時のオブジェクトを、表示用オブジェクトとしてサイズ変更したオブジェクトを設定することになります。  
これにより表示非表示・位置・回転・大きさが変わる異変をプログラミング不要で実現しています。  

異変用のオブジェクトはステップ3で複製して作れば良いと思うので、レベル作成段階ではあまり深く意識しなくても良いかもしれません。  

なお、異変の有無は完全にステージに入ってから（サンプルレベル上のEntryFrontTriggerアクターのエリアに入ってから）視認できるようにしてください。  
入る前から異変が見えてしまって引き返してもシステム上は回答扱いにならず、そのまま進んでしまうと逆走による失敗扱いになる恐れがあります。  
本家「8番出口」でも基本的には角を曲がる直前からでないと異変はわからなかったはずです。  

またサンプルでは異変の反映（ステージの更新）をステージに入ってから行っているため、入り口付近で発生する異変は入った瞬間にオブジェクトが変化してしまい簡単に気が付いてしまいます。  

## 【ステップ2】 異変リスト作成
異変リストはHcbn_DataTable_Anomaliesデータテーブル（/Hachiban/Anomaly/Hcbn_DataTable_Anomalies.uasset）になります。  

![Hcbn_DataTable_Anomaliesの編集画面の図解](https://github.com/user-attachments/assets/d22d9e2b-bf5d-44ce-a3c3-3cdcfc7f011e)

*行の名前（特に使わないので連番でも良いですが、他の行と重複したものは使えません）
*Active（False=チェック無しのものは異変として使われません）
*ID（異変IDで異変有りの時はこの異変IDで異変の制御が行われる）
*Name（異変一覧などに表示されるが、異変のネタバレを避けたい時は抽象的にしても良い）
*Discription（異変一覧に表示される異変の説明・補足）
*Tags（Anomaly.Tag.Difficultを指定した異変は、終盤に優先的表示されやすくなる）

サンプルゲームの異変を参考に、作成したレベルにあった異変を追加していきます。  
サンプル異変も含め使わない異変はActiveのチェックを外せばよいので、まずはアイデア出しのつもりでどんどん思いつく限りの異変を追加しても良いでしょう。  

重要なのはIDで、この異変IDで異変の管理・制御を行います（Active=Falseのチェックが無いものは除く）。  

デフォルトではNameとDiscriptionはゲーム内メニューに表示されますが、その表示個所やボタンを非表示設定に設定にすることは可能です。  
ただNameは開発中のテストプレイ時に発生する異変の名称として画面の左上に2秒ほど表示され便利なので、他の異変と区別できるようにしておきましょう。  

### 異変ID
異変IDにはUnreal Engineのゲームプレイタグ（Gameplay Tag）を使います。  

![ゲームプレイタグの選択・追加の図解](https://github.com/user-attachments/assets/5451b8c8-3840-4297-a44e-e53fb6936c88)

IDの横にある下矢印のボタンを左クリックしてメニューを開き、異変IDにチェックを入れます。  
基本的には新しい異変はIDを追加することになるので、［新しいゲームプレイタグを追加］ボタン（緑色のプラスアイコン）を左クリックします。  
そうすると「名前」「コメント」「ソース」の欄が表示されるので、名前欄に新しい異変IDを入力します。  

異変設定の際に使うので、わかりやすいIDが良いです。  
書式としては「Anomaly.ID.」＋「（わかりやすい名前）」が良いでしょう。  

例えばリンゴの異変であれば「Anomaly.ID.Apple」。
もしリンゴに大きくなる異変と移動する異変があるのなら、「Anomaly.ID.Apple.Big」と「Anomaly.ID.Apple.Move」などにすると良いでしょう。  
こうすると「.」（ピリオド）でグループ化され「Anomaly.ID.Apple」に「Big」と「Move」のタグという形になり便利です。  
もちろん好みで「Anomaly.ID.BigApple」「Anomaly.ID.MoveApple」としても良いです。  

また他に作る異変によっては「Anomaly.ID.Big」や「Anomaly.ID.Move」でグループ化した方が便利な場合もあるでしょうから、ご自身で判断してください。  

コメントに関しては任意で空白のままでも問題はありません。  

そしてソースは「Anomaly.ini」にしておいてください（ゲームプレイタグさえ使えれば良いので別のソースで管理することも可能です）。  
この時、ソース欄右側のお気に入り（星マーク）を有効にしておくと、次回から異変IDを追加する時に自動的に同じソースを選択済みにしてくれるようです。  

「名前」と「ソース」の入力が完了したら、それらの下に表示されている［新しいタグを追加］ボタンを左クリックします。  
追加後はそのIDにチェックを入れ選択します。  

### Tags
ゲームの終盤に発生させたい異変の場合は、Tagsの「Anomaly.Tag.Difficult」にチェックを入れます。  
このタグを持った異変は、終盤に優先的に発生するようになります。  

![異変リストにDifficultタグを設定する方法の図解](https://github.com/user-attachments/assets/cfdff03f-0bbf-4c8a-b1d5-5dbb748d9638)

例えばトラップ系や高難易度異変に設定します。  
ゲームの難易度調整目的以外にも、一目で異変とわかるわかりやすい異変を序盤に発生しやすくするために、あえてそれ以外に設定するという方法もあります。  
ゲーム開始直後は簡単に進めるようにすることで、プレイヤーの気持ちを盛り上げれるかもしれません（ただし終盤にわかりやすい異変が出にくくなるのでどうするかはご自身で判断してください）。  

なおこの終盤発生用タグはHcbn_BP_AnomalyMasterブループリント（/Hachiban/Anomaly/Hcbn_BP_AnomalyMaster.uasset）のDifficultTag変数で設定されたものが使用されます。  

### 異変IDの削除
サンプルの異変IDや誤って作成してしまった異変IDなどは、ゲームプレイタグマネージャーから削除できます。  
ゲームプレイタグ選択メニューの［ゲームプレイタグを管理］ボタンから表示可能です。  

なお未使用の異変IDがあっても、異変リストのActiveが有効（チェック有り）の異変の異変IDしか使われないため、削除しなくても特に問題はありません。  

## 【ステップ3】 異変設定
異変設定にはHcbn_BP_Actor_Anomalyアクター（/Hachiban/Anomaly/Actor/Hcbn_BP_Actor_Anomaly.uasset）を使います。  
エディタ左下の［コンテンツドロワー］ボタンからエクスプローラーのようなメニューを表示できます。  

ここでは例としてサンプルのアルファベットオブジェクトが1つ消える異変を作る場合で説明していきます。  
練習用に異変リストにこの異変を追加しても良いですし、一時的に他の異変IDを流用しても良いです。  

### Hcbn_BP_Actor_Anomalyアクターをレベルに追加する
まずはHcbn_BP_Actor_AnomalyアクターをHcbn_Level_MainStageレベルに配置します。  

![Hcbn_BP_Actor_Anomalyを配置する（メモ含む）図解](https://github.com/user-attachments/assets/b6533aa2-8934-4468-94cc-cb22d4b632b3)

#### メモを書く
異変毎に追加することになるので、どの異変を担当するかがわかりやすいように追加したHcbn_BP_Actor_Anomalyアクターを選択状態にし、そのアクターの詳細のMemoText変数に「アルファベットが消える」のようにどんな異変かわかるようにメモを入力します。  
このメモは開発用でプレイ中は表示されません。  

#### 異変IDを設定する
次にその詳細のAnomalies変数の要素追加ボタン（プラスマーク）を左クリックして項目を追加し、この異変用の異変IDを選択します。  

![Hcbn_BP_Actor_Anomalyに異変IDとHideActorsを設定する図解](https://github.com/user-attachments/assets/adb2f1f3-2a96-41ad-acd1-fdd62b3e72e4)

#### HideActorsを設定する
今回は消える異変のため、詳細のHideActors変数（Hide＝隠す）を使います。  

この変数の要素追加ボタンを左クリックして項目を追加します。  
追加した項目のアクタ選択ボタン（スポイトマーク）を左クリックした後、レベル上の非表示にしたいアルファベットオブジェクトを左クリックします。  

これで設定した異変IDが発生した時に、ここで選択したオブジェクトが非表示になります。  
そのため誤って別のオブジェクトを選択すると、そのオブジェクトが非表示になってしまいます。  

複数のオブジェクトが重なってスポイトで選択できないような時は、リストから選択することもできます。  

#### 応用編 ShowActorsを設定する
もし消える異変ではなく移動する異変の場合は、非表示にするオブジェクトを複製して別の場所に移動させます。  

![Hcbn_BP_Actor_Anomalyで移動する異変を設定する図解](https://github.com/user-attachments/assets/8caeccad-2725-40e6-985b-3a9e0962263e)

そして詳細のShowActors変数（Show＝見せる）に要素を追加し、複製した移動した先となるオブジェクトを選択します。  
これでこの異変が発生した時は、元の場所のオブジェクトが非表示になり、複製した移動後のオブジェクトが表示されるようになります。  

サイズが変わる異変であれば複製したオブジェクトを移動させるのではなく大きさを変えます。  

この要領で表示非表示の切替だけでもアイデア次第で色々な異変を作ることができます。  

### 異変のテスト
設定した異変は、エディタ上でプレイして想定通りに動作するか確認しましょう。  

![ギャラリー設定の場所の図解](https://github.com/user-attachments/assets/ae9fa802-7a01-472c-90ee-9140d1e5be07)

ゲーム内メニュー下部中央のギャラリー設定からテストしたい異変を指定することで強制的にその異変を発生させることができます。  
0ラウンドの異変発生率が0以下だとラウンド1にならないと異変は発生しないので、まずは異変がない状態で対象となるオブジェクトが誤って表示されたり非表示となっていないか確認しつつ、ラウンド1で正常に異変が発生するかを確認します。  

異変抽選後はデバック情報として画面左上に抽選した異変名が2秒ほど表示されるのでそこも見るようにしましょう（開発中のみ表示されます）。  

![デバッグ情報の表示例の図解](https://github.com/user-attachments/assets/9f0f5840-7b73-4650-9165-3625f7be556b)

なお未確認の異変の間（異変が発生した時に異変有りとして回答するまで）は、ギャラリー設定などに異変名は表示されません。  
異変リストのActiveな異変が上から連番になっているため、確認状態になるまではその番号で指定することになります。デバッグ情報として抽選した異変名が表示されるので、そこで正しく異変を指定できているかも確認できます。  

## 仕上げ
エディタ上で最初から最後までプレイでき、クリア後の異変回収なども含めてバグが見つからなければ、一応はゲームが完成したと言えます。  

もし参考用に残している不要なサンプルのオブジェクトなどがあれば削除します。  
基本的にサンプルで使っているHcbn_BP_Actor_Anomalyアクターは何かしらのオブジェクトを参照（HideActorsやShowActorsとして）しているので、先にHcbn_BP_Actor_Anomalyアクターを削除すると削除の際にメッセージが表示されないと思います。  

念のため、誤って削除したオブジェクトないか最後にテストしておいた方が安心です。  

### ゲーム情報の書き換え
ゲーム公開前にゲームタイトルなどを自分のゲーム用に書き換えます。  

ゲームタイトルに関しては商標登録の有無に関係なく、「N番出口」など特に本家「8番出口」の続編などと誤認させる恐れがあるものは避けましょう。  
続編と誤解してプレイする人がいるだけでなく、誤解したまま本家の開発者さんにクレームが行くケースなども普通にありえます（世の中のみんなが賢いわけではありません）。  

ゲームタイトルがシンプルだと検索した時に埋もれてしまうことがあるので、短い単語の組み合わせの時は注意した方が良いかもしれません。  
またセンシティブな単語が含まれるとYouTubeなどでは不都合があるため、ゲーム実況を想定する場合はその点にも注意が必要です。  

#### プロジェクト設定
エディタ上部のメニューの［編集 > プロジェクト設定］を左クリックし、プロジェクト設定の［プロジェクト > 説明］を開き、［Unreal Editorについて > プロジェクト名］と［表示 > プロジェクトが表示されたタイトル］にゲームタイトルに入力します（ゲーム起動時のウィンドウ名に使用される）。  

なお、［Unreal Editorについて > プロジェクト名］はWindowsのタスクマネージャーのアプリの表示で影響があるようです。  
他の項目は特に変更しなくても問題ないかもしれませんが、［Unreal Editorについて > プロジェクトバージョン］が未入力だとパッケージ化の際などにエラーが発生し失敗するようです。  

![プロジェクトが表示されたタイトルの設定個所（プロジェクトバージョン含む）の図解](https://github.com/user-attachments/assets/e1984839-651f-4383-a8b4-4fa49630fa0a)

### Hcbn_BP_FunctionLibrary
* Title（ゲームタイトル）
* Version（バージョン）
* Copyright（著作権表記）
* Year（リリース年）

ゲーム内ではこれらの情報がHcbn_BP_FunctionLibrary（/Hachiban/Blueprint/Hcbn_BP_FunctionLibrary.uasset）のGetGameInfo関数のReturnNodeにまとめているので、ここも書き換えてください。  

![Hcbn_BP_FunctionLibraryのGetGameInfo関数の編集箇所の図解](https://github.com/user-attachments/assets/b7fbcdd0-6f7c-497d-93b4-3859e01457d8)

リリースするまでは「ver.01.00.00」としておいて問題ないと思います。  
ちょっとした修正のアップデートであっても、その都度バージョンを繰り上げておくと不具合に関する問い合わせがあった時などに便利です。  

#### クレジット表記
GetOtherCredit関数のReturnNodeのReturnValueにクレジット表記を入力しておくと、ゲーム内メニューのインフォメーションのクレジットタブと、クリア時に表示されるUIに自動的に表示されます。  

![Hcbn_BP_FunctionLibraryのGetOtherCredit関数の編集箇所の図解](https://github.com/user-attachments/assets/c9d43594-0656-4e9c-8c77-fa38129de04f)

公式ストアであるUnrealマーケットプレイスで入手したアセットは特に必要ないのですが、フリー音源などをゲーム素材に使用する場合は規約に従ってクレジット表記などが必要になる場合があります。  
フリー素材は規約に従った場合に無料で使えるものなので、規約を守らない場合は料金が発生したり著作権法上の法的責任を問われる場合があるので注意してください。  

このゲームのテンプレート（MITライセンス）とUnreal Engineの表記はゲームタイトルとリリース年を元に自動表示しているので、特に問題がなければ編集せずにそのまま表示してください。  

### インフォメーションの概要
ゲーム内メニューのインフォメーションの概要の文言を変更する場合はHcbn_Advance_RichTextBlock_Info_Summaryファイル（/Hachiban_Advance/UI/Info/Hcbn_Advance_RichTextBlock_Info_Summary.uasset）の［コンテンツ > Text］を書き換えてください。  

![Hcbn_Advance_RichTextBlock_Info_Summaryの編集箇所の図解](https://github.com/user-attachments/assets/855b90a8-3f4d-4ab8-9cb1-382b9ee8e453)

簡単なゲームの説明やゲーム実況の許可などについて書いても良いでしょう。  
なお、ゲーム内だけでなくストアページでもそうですが、説明を読まない人もいるのでその点は注意・諦めましょう。  

# パッケージ化（配布用ファイル作成）
エディタ上で問題なくゲームを遊ぶことができても、このままでは他の人にプレイしてもらうには問題があります。  

特にアセットを使用している場合、無料アセットであってもプロジェクトファイルをそのまま配布するとライセンス違反の恐れがあります。  
基本的にアセットはゲームファイルに変換して再利用できない状態で配布する場合のライセンスが付与されています。  

そのため作ったゲームをパッケージ化して配布用のファイルを作成しなければなりません。  

Unreal EngineはWindowsだけでなく、MacやiOS（iPhone/iPad）、Android、PlayStation、Switchなど様々なプラットフォーム向けにパッケージ化できます。  
しかしどのプラットフォーム向けにパッケージ化するにしても、そのプラットフォーム向けに別途インストールするなどの準備が必要です。  

もしすでにUnreal Engineでゲームを開発していてパッケージ化の準備が完了しているのであれば、すぐにパッケージ化できるかと思います。

ただパッケージ化に関してはこのゲームのテンプレート固有のテーマではないため、詳しいパッケージ化の手順などについては公式ドキュメントや動画などを参考にしてください。  

「UE5 パッケージ化」などのキーワードでネットや動画を検索してみてください。  
なおUnreal Engineのバージョンや開発環境がWindowsかMacなどかによって必要なものや手順が異なることがあるため、1つの情報だけでは上手くできない可能性があります。  

なおこのゲームのテンプレートはWindows11上で開発し、Windows向けにエラーも警告もなくパッケージ化でき、正常に動作することは確認できています。  
警告に関しては使用するアセットが起因するものもありゼロにできないこともありますが、警告があっても配布ファイル作成には特に問題はないと思います（エラーがある場合はパッケージ化が失敗すると思います）。  

もしパッケージ化が失敗する場合、まずはこのゲームのテンプレートを編集せずにそのままパッケージ化を試してみても良いかもしれません。  
この時点で失敗する場合はパッケージ化の準備が不十分であると考えられますし、成功する場合は編集した自作ゲーム側に問題があると考えられます。  

なおパッケージ化に関しては普通にプログラミングできる人でも苦戦することは珍しくない躓きポイントですので、上手くいかなくてもあまり気にする必要はありません。  
ゲーム開発者でもパッケージ化経験がない人は少なくないでしょうし、そもそもゲームを完成することなく頓挫することも珍しくはありません。
そのためにパッケージ化に関する情報自体が少ないです。  

## パッケージ化の手順
Windows向けのパッケージ化の準備が完了している場合、次の手順でパッケージ化可能です。  
なお、細かい設定を行うことでパッケージ化したファイルを小さくしたり暗号化したりもできますが、ここでは割愛します。  

![パッケージ化ボタン位置の図解](https://github.com/user-attachments/assets/2d48d959-0b6d-4967-9362-d6f686449a60)

エディタ上部中央の［プラットフォーム］ボタンを左クリックしてメニューを開き、［コンテンツ/SDK/デバイス管理 > Windows］を開きます。  
この時、［Windows］の前にビックリマークアイコンが表示されている場合はパッケージ化の準備が完了していないと思われます。  
そして［バイナリ コンフィギュレーション > シッピング］が有効（白い点）になっていなければ、それを左クリックして有効にしてください。  
［シッピング］が有効であれば、［コンテンツ管理 > プロジェクトをパッケージ化］を左クリックしてください。  
保存先のディレクトリを聞かれるので、パッケージ化用にわかりやすいフォルダを作って指定します。  

これでパッケージ化の処理がはじまります。  

パッケージ化時間はゲームの内容と開発端末（おそらくCPU性能）の性能で大きく異なります。  
未編集状態のこのゲームのテンプレートであれば、AMD Ryzen 9 16コア環境で1分程度でした。
しかし過去に数世代前のCPUでゲーム開発していた時は、ゲームのサイズも大きく初回のパッケージ化は10時間程掛かりました（2回目以降は数十分に短縮されました）。

完了後は成功しても失敗しても音で通知してくれるはずです。  

パッケージ化が成功していれば、指定したフォルダに「Windows」フォルダができていて、その中に配布用ファイル一式がまとめっていると思います。
配布する時はそのWindowsフォルダをZIP化するなどして公開すると良いでしょう（Steamなどのストアで公開する時は、ストアの指示に従ってください）。  

![パッケージ化で作成されたファイル一式の図](https://github.com/user-attachments/assets/cce5bb8b-3f57-47c2-9fda-4647741e2b69)

設定などを変更していなければ「HachibanMake.exe」をダブルクリックすればゲームが起動するはずです。  
実は恐ろしい話ですが、エディタ上では問題なく動作していても、パッケージ化すると動作しなくなることがあるので、配布用のファイルでもテストプレイが必要です（ゲームエンジンそのものにもバグはあるのです）。  

### ゲームの実行ファイルのアイコン
初期設定ではパッケージ化したゲームのEXEファイルのアイコンはUnreal Engineのマークになっています。  

これを変更する場合はエディタの「プロジェクト設定」の［プラットフォーム > Windows > Icon > ゲームアイコン］を変更するだけです。  
ファイル形式はIcoファイル（*.ico）ですが「PNG Ico 変換」などで検索すれば無料でファイル変換してくれるサービスが見つかるかと思います。  
画像の寸法は256pxの正方形のようです。  

# 応用編

## メニューをカスタマイズ
ゲーム内メニューは主にHcbn_Advance_WBP_Pause_Contentウィジット（/Hachiban_Advance/UI/Pause/Hcbn_Advance_WBP_Pause_Content.uasset）の編集でカスタマイズ可能です。  

### 不要な項目を消す
例えば異変一覧を表示しないのであれば、Hcbn_Advance_WBP_Pause_Contentウィジットの「デザイナー」（エディタ右上の［デザイナー］［グラフ］ボタンで切替）から、［異変一覧］ボタンを選択し、右側の詳細の［動作 > Visibility］を「Collapsed」に変更するだけです。  
これでゲーム内メニューを開いても［異変一覧］ボタンは表示されなくなります。  
この時に「Hidden」を選んでも非表示になりますが、この場合は本来その項目が表示されたはずのエリアが残ったままの歯抜け状態になります。好みに応じて使い分けてください。  

![Hcbn_Advance_WBP_Pause_Contentの項目非表示方法の図解](https://github.com/user-attachments/assets/1e4a0f5a-0b0e-473a-a9bd-06d7f6d065f7)

この要領で他の表示したくない項目も非表示にできます。  
例えばモード変更機能をなくしたり、ギャラリー機能を無くすなんてことも可能です（ギャラリー機能は開発中の異変のテストで便利なのでリリース時に非表示にすると良いでしょう）。  

## プレイヤーのパラメーター
プレイヤーの移動速度やジャンプ力などはコントローラーかプレイヤーのブループリントのパラメーターで変更します。  
これはあくまでもこのゲームのテンプレートの場合であって、使用するキャラクターやライブラリなどによっても異なります。  

なおパラメーター値を0にすることで無効化することもできますが、その時は必要に応じてメニュー内の操作方法を編集したり、そもそも操作方法ボタンを非表示にしてストアページなどで説明に切り替えることもできます（そもそもゲーム内の説明を読まないプレイヤーもいれば、ストアページの説明を読まないプレイヤーもいます）。  

### プレイヤーコントローラー（歩く速度・走る速度））
コントローラーのパラメーター変更はHcbn_Advance_BP_Controller_Helper_ActorComponentブループリント（/Hachiban_Advance/Blueprint/Controller/Helper/Hcbn_Advance_BP_Controller_Helper_ActorComponent.uasset）で行います。  

画面中央上部の［クラスのデフォルト］ボタンを左クリックし、右側の詳細タブの次変数を変更します。  

* SprintSpeed（走る速度）
* WalkSpeed（歩く速度）

### キャラクター（カメラの高さ・ジャンプ力）
キャラクターのパラメーター変更はHcbn_BP_Characterブループリント（/Hachiban/Blueprint/Character/Hcbn_BP_Character.uasset）で行います。  

画面中央上部の［クラスのデフォルト］ボタンを左クリックし、右側の詳細タブの次変数を変更します。  

* BaseEyeHeight（カメラの高さ）
* JumpZVelocity（ジャンプ力）

## 国際化（多言語対応）
Unreal Engine標準の[ローカリゼーションダッシュボート](https://dev.epicgames.com/documentation/ja-jp/unreal-engine/localization-tools-in-unreal-engine?application_version=5.4)を使ってゲーム内メニューの国際化に対応しています（エディタ上部の［ツール > ローカリゼーションダッシュボート］を左クリックして開けます）。  

ただ異変リストに追加した異変名や異変詳細はこのローカリゼーションダッシュボートを使って翻訳したものを追記していく必要があります。  

国際化対応が難しかったり負担が大きい場合は、割り切って異変名や異変詳細の国際化はあきらめても大きな問題はないでしょう。  
また国際化対応自体をやめる場合は、ゲーム内メニューと環境設定にある言語設定の項目を非表示にしてください。  

なおエディタ上で言語の切替の動作確認を行う場合は「スタンドアローンゲーム」としてプレイする必要があるようです（これ以外のモードでテストしてしまうとエディタの表示言語が変更されてしまう恐れがあります）。  

### デカール（ゲーム内オリジナルポスターの作り方）
サンプルの禁煙や広告のポスターはDecal（デカール）で表示しています。  
デカールはデコボコした表面にも画像を表示することが可能で、レベル内に画像を表示する時に便利な方法の1つです。  

まずゲーム内に表示する画像ファイルをTextureフォルダ（/Hachiban/Texture）などわかりやすいフォルダにドラッグ＆ドロップなどでインポートします。  

次にベースとなるデカール用のHcbn_M_Decal_Posterマテリアル（/Hachiban/Material/Decal/Hcbn_M_Decal_Poster.uasset）を右クリックしてメニューを表示し、その中の［マテリアルインスタンスを作成］を左クリックします。  
自動的に同じフォルダ内に「Hcbn_M_Decal_Poster_Inst」などの名前のマテリアルインスタンスが作成されるので、まずはわかりやすい名前に変更しておきましょう。  

![Hcbn_M_Decal_Posterからマテリアルインスタンを作成する図解](https://github.com/user-attachments/assets/fd69af37-c758-41f1-8bd8-9aaedebdbb54)

そしてこのファイルをダブルクリックして開きます。  
開いたら、右側の詳細タブの［パラメータ グループ > Global Texture Parameter Values］の［Tex］をチェック有の状態にし、その右側の項目に先程インポートした画像を指定します。  

![Hcbn_M_Decal_Posterのインスタンスマテリアルに画像を設定する箇所の図解](https://github.com/user-attachments/assets/c4719b2a-f85c-4e98-bc91-43cc9f41af86)

後はレベル内にこのマテリアルインスタンスをドラッグ＆ドロップで配置するだけです。  
恐らくデカールの画像が大きく表示されると思うので、そのデカールを選択状態にし、詳細タブの［デカール > Decal Size］でサイズを調整し、好みの場所と角度で配置してください。  

![レベル上でデカールのDecalSize変更箇所の図解](https://github.com/user-attachments/assets/0fed3265-6382-4dee-a24b-72989c24a5db)

## ゲームの画質について
初期設定ではUnreal Engineの高画質なグラフィックが有効になっており、処理負荷が高く、低スペックなプレイ環境では快適性が犠牲になってしまいます。  
特に「Lumen」の影響が大きいと思われます。  

LumenはUnreal Engine 5の新機能で、完全に動的なグローバルイルミネーションおよび反射のシステムです。  
これにより自動に光と影がリアルに近い表現となり、初心者でもそれなりに見栄えの良いグラフィックのゲームを作れるようになります。  

Lumenは次世代コンソールやハイエイド環境向けに設計されており、PlyaStation 5やXbox Series Xやそれに匹敵する性能のゲーミングPC向けになっています。  
まだまだLumenの開発は継続されていますが、現状では60FPSを安定的に出すことすら簡単ではないのが現状のようです。  

Lumenを無効化すれば大幅に負荷を軽減できるのですが、グラフィックをかなり犠牲することになります。  
ポストプロセスなどで対応可能のようですが、それには知識・スキルが必要になるようです。  

Lumenを無効化した場合のイメージとしては、[Nintendow Switch版「8番出口」](https://www.youtube.com/watch?v=AlGNtXqMK_c)が参考になるかもしれません。
Switch版とPC版の「8番出口」の見た目が明らかに異なっているかと思いますが、これはLumenがそもそもSwitchに対応しておらず、Lumenが無効になっているためと思われます。

一応、ゲーム内環境設定の5段階の画質設定でLumenを有効にしつつ各種パラメーターを調整して画質とパフォーマンスのバランスを図ってはいます。
しかし、低スペック環境では厳しいのが現状です。  
さらにゲーム実況・VTuberが実況する場合は、録画・配信ソフトやアバターの処理負荷もあり、ミドルクラスのプレイ環境でも画質を下げないとパフォーマンスに影響が出ることがあります。  

そもそもゲームのパフォーマンスチューニングには知識・スキルが求められるものなので、はじめは画質を犠牲にするか要求スペックを高くする判断も必要かもしれません。  

### 画質のカスタマイズ
特に画質にこだわらない、もしくは画質を妥協してでも要求スペックを下げたい場合、大きく2つの対応方法があります。  

* プロジェクト設定
* ゲーム内画質設定（上級者向け）

#### プロジェクト設定
プロジェクト設定はエディタ上部の［編集 > プロジェクト設定］を左クリックで開きます。  
なおプロジェクト設定から色々な変更を行えますが、影響範囲が大きいものもあるためよくわからないで変更しないように注意してください。  

簡単な画質（負荷軽減）に関係する項目を紹介します。  

##### ターゲットハードウェア
プロジェクト設定の［プロジェクト > ターゲットハードウェア］を開きます。  
デフォルトでは「Desktop」「Maximum」と最高設定になっているので必要に応じて下げてみてください（変更後はプロジェクト設定に指示に従ってエディタの再起動が必要になると思います）。  

![プロジェクト設定のターゲットハードウェアの設定個所の図解](https://github.com/user-attachments/assets/993b3a04-3303-4c95-93e2-9c759caa16d0)

##### アンチエイリアス手法
アンチエイリアスは曲線などをボカして綺麗に見せる処理です。  
当然、品質重視にすると負荷は高くなります。  

プロジェクト設定の［エンジン > Rendering］を開き、［Default Settings > アンチエイリアス手法］から設定可能です。  

![アンチエイリアス手法の設定個所の図解](https://github.com/user-attachments/assets/321bdaef-f181-4bf5-ad36-30999d288fa7)

初期設定の「TSR」は負荷が高く「TAA」「FXAA」「None（アンチエイリアス無し）」の順に負荷が下がります（画質も下がる）。  
※「MSAA」はよくわかりませんでした。

#### ゲーム内画質設定（上級者向け）
ゲーム内メニューの環境設定で画質を5段階から選択できるようになっていますが、そこで行われる画質設定はHcbn_Advance_BP_GraphicSettingComponentアクターコンポーネント（/Hachiban_Advance/Component/GraphicSetting/Hcbn_Advance_BP_GraphicSettingComponent.uasset）で切り替えています。  

このファイルをダブルクリックして開き、エディタ上部中央あたりに表示される［クラスのデフォルト］ボタンを左クリックします。  
そして右側に表示される詳細タブの［デフォルト > Quality Mapping］に5つのマップエレメントがあり、この5つが5段階の画質設定と紐づいています。  

* 1 = 最低画質
* 3 = 低画質
* 5 = 標準画質
* 7 = 高画質
* 9 = 最高画質

![Hcbn_Advance_BP_GraphicSettingComponentのQualityMapping設定個所の図解](https://github.com/user-attachments/assets/8bfff607-575e-4b46-b563-86760ea8493b)

そして画質別にUnreal EngineのGameUserSettingsで指定できる画質の値をプリセットとして設定しています。  
なおこれらの値を下げると顕著に画面表示に影響することがあり、中にはゲームプレイに影響しかねないので、画質を下げる変更を行う時はテストプレイで変化を確認するようにしてください。特に明るい所や暗い所、一部のエフェクトでのみ変化が顕著になることがあるので、影響がありそうな箇所は特に注意してください。  

比較的簡単に変更できる項目は「ResolutionScaleNormalized」です。  
数値を下げると動画の解像度を下げた時のように、単純に画面が荒くなります。  

また5段階の画質ごとに「PostProcessVolume」を設定できるので、ここで「Lumen」の無効化もできます。  

## 他システムとの統合（上級者向け）
既にアセットや自作ゲームの共通システム（ゲーム内メニューなど）がある場合、統合しやすいようにサンプルゲームは主要箇所のみを使うことができるようになっています。  

具体的には異変管理のコアである「Hachixit」ディレクトリと、異変探しゲームのコアである「Hachiban」ディレクトリです。  
これらだけで動作させる場合はGameModeを「Hcbn_BP_GameMode」にし、GameInstanceを「Hcbn_BP_GameInstance_Anomaly」に変更することで動作確認が可能です。  

この場合はサンプルのゲーム内メニューを使わなくなります。そのためギャラリー設定もできなくなり、画質やマウス感度の設定などもできなくなります。  
あわせて進行状況のセーブ・ロードもされなくなるため、必要ならセーブ・ロードの実装が必要になります。  

なお「Hachiban_Advance」ディレクトリはゲーム開発の入門・初心者用にゲーム内メニューなど追加したものになっています。  
ただしプログラム自体は複雑なためカスタマイズは上級者向けとなっています。  

そして「Lelool」ディレクトリは別ゲームなどでも使うための共通システムで、「Hachiban_Advance」ディレクトリは「Lelool」ディレクトリに依存しています。  

また各ディレクトリのファイルは、基本的にディレクトリ毎に共通したプレフィックスがついています。  

* Hachixit（依存なし） = Hcxt_
* Hachiban（「Hachixit」に依存） = Hcbn_
* Hachiban_Advance（「Hachiban」と「Lelool」に依存） = Hcbn_Advance_
* Lelool（依存なし） = Lelool_

## フォント
Unreal Engine標準のフォントは日本語対応にはなっていますが、日本人からすると不自然に感じるものが一部あります。  
フォントをゲームに組み込むことも可能ですので、余力があれば自作ゲームに組み込んでも良いかもしれません。  

# 発展編
このゲームのテンプレートではプログラミング不要で8番ライクゲームを作れはしますが、作れる異変は表示・位置・角度・大きさの組み合わせだけの異変しか作れず物足りないかも知れません 

もっと面白くしたい、もっと魅力的にしたいと動きのある異変やプレイヤーの行動に反応する異変を作りたいと思うのなら、ステップアップとしてゲーム開発の世界にもっと足を踏み入れてください。  
よりゲーム開発に興味や探求心を持ってもらうことがこのゲームのテンプレートの狙いでもあります。  

8番ライクゲームのルールを変更（異変を見つけたら銃で撃つや、異変を見つけたら左に見つからなかったら右に進むなど）するのは上級者向けですが、動きのある異変はその内容次第ですがゲーム開発・プログラミング初心者でも挑戦しやすいと思います。  

例えば8番出口のおじさんのようなキャラクターを歩かせる場合、キャラクターの表示方法と歩かせ方が分かれば、それをレベル上に配置するだけです。  
そのキャラクターに異変を発生させたければ、通常のキャラクターと異変があるキャラクターの両方を配置し、これまでの異変設定の要領で異変IDをそれぞれのキャラクターを設定するだけです。  

## トラップアクター
動きのある異変の参考としてHcbn_BP_Actor_Anomaly_Trapアクター（/Hachiban/Anomaly/Actor/Trap/Hcbn_BP_Actor_Anomaly_Trap.uasset）があります。  
サンプルゲームの棘の罠の異変になります。  

レベル上に配置したトラップ用のトリガーをこのアクターのTrigger変数に設定しており、このトリガーにプレイヤーが触れると失敗処理を実行するようになっています。  

この罠を動かしたり細い道の下に広げたりすればアクション要素を追加できますし、プレイヤーを襲うキャラクターに連動すれば捕まるとダメな異変になります。  

プログラミングした異変用アクターやトリガーにも異変として設定することで、異変がある時のみ表示・実行させることができます。  

## 8番ライクゲームのルールを変更する（上級者向け）
このゲームではゲーム開発初心者が困らないよう本家「8番出口」と同様の「異変を見つけたら引き返し、異変が見つからなかったら引き返さない」を初期設定にしています。  

追加のプログラミングにより「異変を見つけたら左に、異変が見つからなかったら右に進む」といったルールにすることは可能です。  
より上級者向けですが、異変を見つけたら銃で撃つといったルールにすることもできます。  

ルール変更はHcbn_BP_LevelHelper_MainStageの変更で実現できるとは思いますが、複雑かつその変更内容に不具合があるとゲーム進行に影響があるのでかなり上級者向けかもしれません。  
そして上級者であっても、複雑なシステムの仕様変更は高難易度かつハイリスクです。このゲームのテンプレートを作った本人ですら仕様変更は気軽にできないものです。  

# ゲーム作成・異変作成時の注意点

## 色の識別は避ける（アクセシビリティ）
赤と青を見分けるのが苦手など、色の識別が苦手な人は少なくありません（日本人男性20人に1人の割合でいると言われています）。  
またディスプレイなどプレイ環境でも見え方が異なることもありえます。  

色の違いの異変だけでなく、異変の有無で青い道と赤い道を選ばせるような時は色以外でも区別できるオブジェクトなどを配置するようにしましょう。  

## 小さな位置・角度・サイズだけの変化は避ける
ゲーム画面上では小さな位置・角度・サイズの変化の視認は難しく、せめて閉じていたドアや目などが開くような意味を伴わないと認識が難しいです。  
そのためゲームのアニメーションでは現実の関節の可動域を超えてオーバーに動かすぐらいです。  

## 無音プレイを想定する
外出先などノートPCやスマートフォンなどでプレイする場合は、無音でプレイしていたり電車などの騒音でかき消されたりする可能性があります。  
そのため音だけでしか認識できない異変などは避けた方が良いでしょう。   

# よくある質問
このゲームのサンプルはライセンスが非常に緩いMITライセンスで公開しており、ライセンスを守ってライセンス表記さえすれば非常に自由度が高いです。  
もちろん、他に併用するライブラリなどがある場合はそれらのライセンスの確認は必要です。  

## サンプルゲームをゲーム実況しても良いですか？
問題ありません。  

## このゲームのテンプレートで作ったゲームを有料で販売しても良いですか？
問題ありません。  

## このゲームのテンプレートで作ったゲームのソースコードは非公開でも良いですか？
問題ありません。  

## このゲームのテンプレートの有料教材を作っても良いですか？
問題ありません。  

## このゲームのテンプレートを有料の勉強会の教材に使っても良いですか？
問題ありません。  

## このゲームのテンプレートで8番ライク以外のゲームを作っても良いですか？
問題ありません。  

## このゲームのテンプレートの一部を別のゲームに流用しても良いですか？
問題ありません。  

## エディタのレイアウトが変になってしまったのですが？
エディタ上部の［ウィンドウ］から［レイアウトをロード > デフォルトのエディタレイアウト］を左クリックすれば、エディタのレイアウトが初期状態に戻ります。  

![デフォルトのエディタレイアウトに戻すための項目の位置の図解](https://github.com/user-attachments/assets/dfd929d4-1182-45d9-938d-819f5c994c7a)
