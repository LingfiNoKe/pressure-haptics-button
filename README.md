# pressure-haptics-button
感圧スイッチとハプティクスを用いた新しいゲーム用ボタン
# 高速入力のための感圧スイッチとハプティクスを使ったボタンの提案

**導入**

既存の入力デバイスの課題

最近は磁気キーボードスイッチとラピッドトリガーと呼ばれる高速入力のための機能がある。

従来のメカニカルスイッチとの違い:

従来のメカニカルスイッチは、キーを押し込んでから、一定の深さまで移動した時点で入力が認識されます。この入力が認識される深さを「アクチュエーションポイント」と呼びます。

その後、再び入力が行える状態にするためには、キーを一定の位置まで戻す必要があります。このキーがリセットされる深さを「リセットポイント」と呼びます。

メカニカルスイッチでは、アクチュエーションポイントとリセットポイントが固定されており、キーを繰り返し入力するためには、アクチュエーションポイントまで押し込み、さらにリセットポイントまで戻すという、一定の距離の移動が必要でした。

ラピッドトリガーの仕組み:

ラピッドトリガーでは、このリセットポイントが固定されていません。

キーが上に戻る方向に動き始めたら、すぐにリセットされるように設定されているため、キーの移動距離を最小限に抑え、高速な入力が可能になります。

つまり、従来のメカニカルスイッチでは、

*   キーをアクチュエーションポイントまで押し込む
*   キーをリセットポイントまで戻す

という動作が必要だったのに対し、ラピッドトリガーでは、

*   キーをアクチュエーションポイントまで押し込む
*   キーが上方向に少しでも動き始めれば、すぐにリセットされる

という動作だけで、次の入力を受け付けられるようになります。

また、アクチュエーションポイントについても磁気キーボード等は極めて浅いアクチュエーションポイントを設定できる。

しかし、磁気スイッチとラピッドトリガーの併用には、リセットポイントが入力位置のすぐ上にあるという構造的な特徴が、常に入力状態を維持したい場合に課題となります。このため、意図せずリセットポイントを通過しないように常にキーを押し続ける必要があるものの、磁気キーボードスイッチには物理的なストロークがあり、それを超えて入力することはできません。つまり、押し続ける必要があるにも関わらず、押し続けると物理的なストロークの制約により、それ以上押し込めないことになります。

図1に示されるように物理的なスイッチの例として0.4Nで移動し始め0.6Nで底打ちをするスイッチと、感圧スイッチでは同じようなアクチュエーションポイントや、ラピッドトリガーの設定でもoffになるタイミングが違うことがわかります。

**構成部品と構成**

本提案のボタンは、主に以下の構成部品から構成されています。

1.  **ボタン筐体:**
    *   ボタン全体を覆い、内部部品を保護する役割を果たします。
    *   感圧センサーや振動モーターなどを固定するための機構を備えています。
    *   操作性を考慮した形状、材質が用いられます。
2.  **感圧センサー:**
    *   ボタンに加えられた圧力を検知し、その値を電気信号に変換します。
    *   ボタンの押し込み具合に応じて、アナログ的な入力が可能になります。
    *   微細な力も検知可能な高精度のものが採用されます。
3.  **ハプティクス用振動モーター:**
    *   電気信号に基づいて振動を生成し、触覚フィードバックを提供します。
    *   ボタンを押した際のフィードバックや、ゲーム中のイベントに合わせた振動を生成できます。
    *   振動パターンや強度を細かく制御でき、ONとOFFのタイミングをユーザーにフィードバックすることができます。
4.  **制御回路 (マイコン):**
    *   感圧センサーからの電気信号を読み取り、ハプティクスモーターを制御します。
    *   PCやゲーム機との接続インターフェースを担い、データの送受信を行います。
    *   高速なデータ処理が可能なマイクロコントローラーが用いられます。

図2に示すように、これらの構成部品は以下の様に接続されています。

*   ボタン筐体には、感圧センサーとハプティクスモーターが内蔵されています。
*   感圧センサーとハプティクスモーターは、制御回路（マイコン）に接続されています。
*   制御回路（マイコン）は、PCやゲーム機に接続されています。

これにより、ボタンに加えられた力が感圧センサーで電気信号に変換され、その信号が制御回路に送られることで、ハプティクスモーターが振動を生成します。また、制御回路は、感圧センサーの信号をもとにPCやゲーム機に送信し、その信号によってゲーム内での操作を実現します。

**技術の強み**

感圧センサーとハプティクスを組み合わせることで、強くボタンを押した状態からでもラピッドトリガーのメリットを享受することができ、なおかつハプティクスによるフィードバックにより、磁気キーボードとラピッドトリガーを組み合わせたキーボードでは、リニアに動くスイッチの途中にアクチュエーションポイントやリセットポイントがあるため、そもそもONとOFFのタイミングをフィードバックすることができなかった点を補完し、ユーザーが自分の行動をより明確に理解することができる。
さらに、この技術はラピッドトリガーとの組み合わせにおいて、物理ストロークによる制約がない為、ストロークを超える入力を妨げることなく高速入力が可能になります
