from pathlib import Path

html = r'''<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="theme-color" content="#11131a" />
  <title>Cocktail Party｜公式ゲーム説明書</title>
  <meta name="description" content="おすしファクトリー制作のパーティーゲーム『Cocktail Party』公式ゲーム説明書。" />

  <style>
    :root{
      --bg:#101219;
      --bg2:#171a23;
      --card:#1d202b;
      --card2:#232735;
      --text:#f7f2e8;
      --muted:#b9b4aa;
      --gold:#e6c26e;
      --gold2:#b88b35;
      --line:rgba(255,255,255,.10);
      --shadow:0 18px 60px rgba(0,0,0,.28);
      --radius:22px;
    }

    *{box-sizing:border-box}
    html{scroll-behavior:smooth}
    body{
      margin:0;
      font-family:
        -apple-system,BlinkMacSystemFont,
        "Hiragino Kaku Gothic ProN","Yu Gothic","YuGothic",
        "Noto Sans JP","Segoe UI",sans-serif;
      color:var(--text);
      background:
        radial-gradient(circle at 20% 0%, rgba(230,194,110,.10), transparent 30%),
        radial-gradient(circle at 100% 20%, rgba(152,103,178,.10), transparent 24%),
        linear-gradient(180deg,#0d0f15 0%,#141721 100%);
      line-height:1.8;
    }

    a{color:inherit}
    img{max-width:100%}

    .wrap{
      width:min(1100px,calc(100% - 36px));
      margin:0 auto;
    }

    .topbar{
      position:sticky;
      top:0;
      z-index:50;
      backdrop-filter:blur(14px);
      background:rgba(12,14,20,.78);
      border-bottom:1px solid var(--line);
    }

    .topbar-inner{
      min-height:68px;
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:18px;
    }

    .brand{
      display:flex;
      align-items:center;
      gap:12px;
      text-decoration:none;
      font-weight:800;
      letter-spacing:.02em;
    }

    .brand-mark{
      width:36px;
      height:36px;
      border-radius:50%;
      display:grid;
      place-items:center;
      color:#17120a;
      background:linear-gradient(135deg,#f7dd93,#b7842a);
      box-shadow:0 6px 24px rgba(230,194,110,.24);
      font-size:18px;
    }

    nav{
      display:flex;
      gap:8px;
      flex-wrap:wrap;
      justify-content:flex-end;
    }

    nav a{
      text-decoration:none;
      color:var(--muted);
      font-size:13px;
      padding:8px 11px;
      border-radius:999px;
    }

    nav a:hover{
      color:var(--text);
      background:rgba(255,255,255,.06);
    }

    .hero{
      padding:86px 0 62px;
      position:relative;
      overflow:hidden;
    }

    .hero-grid{
      display:grid;
      grid-template-columns:1.15fr .85fr;
      gap:52px;
      align-items:center;
    }

    .eyebrow{
      display:inline-flex;
      align-items:center;
      gap:8px;
      color:var(--gold);
      border:1px solid rgba(230,194,110,.30);
      background:rgba(230,194,110,.07);
      border-radius:999px;
      padding:7px 12px;
      font-size:12px;
      font-weight:700;
      letter-spacing:.08em;
      text-transform:uppercase;
    }

    h1{
      margin:20px 0 14px;
      font-family:Georgia,"Times New Roman",serif;
      font-size:clamp(52px,8vw,98px);
      line-height:.95;
      letter-spacing:-.045em;
    }

    .jp-title{
      font-size:clamp(18px,2.6vw,28px);
      font-weight:800;
      color:var(--gold);
      margin-bottom:18px;
    }

    .lead{
      font-size:clamp(17px,2.2vw,21px);
      color:#eee7da;
      max-width:680px;
      margin:0;
    }

    .sublead{
      color:var(--muted);
      margin-top:14px;
      max-width:680px;
    }

    .hero-actions{
      display:flex;
      flex-wrap:wrap;
      gap:12px;
      margin-top:28px;
    }

    .btn{
      display:inline-flex;
      align-items:center;
      justify-content:center;
      min-height:48px;
      padding:0 18px;
      border-radius:14px;
      text-decoration:none;
      font-weight:800;
      font-size:14px;
      transition:.2s ease;
    }

    .btn-primary{
      color:#18130b;
      background:linear-gradient(135deg,#f3d98d,#be8d34);
      box-shadow:0 10px 28px rgba(190,141,52,.22);
    }

    .btn-secondary{
      border:1px solid var(--line);
      background:rgba(255,255,255,.04);
      color:var(--text);
    }

    .btn:hover{transform:translateY(-2px)}

    .glass-card{
      min-height:440px;
      border-radius:32px;
      background:
        radial-gradient(circle at 50% 20%,rgba(255,255,255,.08),transparent 34%),
        linear-gradient(145deg,#212533,#11131a);
      border:1px solid rgba(255,255,255,.11);
      box-shadow:var(--shadow);
      display:grid;
      place-items:center;
      padding:34px;
      position:relative;
      overflow:hidden;
    }

    .glass-card::before{
      content:"";
      position:absolute;
      width:230px;
      height:230px;
      border-radius:50%;
      background:rgba(230,194,110,.08);
      border:1px solid rgba(230,194,110,.22);
      top:-72px;
      right:-42px;
    }

    .cocktail{
      width:min(280px,85%);
      aspect-ratio:1/1.12;
      position:relative;
      display:grid;
      place-items:center;
    }

    .cocktail .bowl{
      width:70%;
      height:35%;
      border:5px solid var(--gold);
      border-top:none;
      clip-path:polygon(0 0,100% 0,62% 100%,38% 100%);
      position:absolute;
      top:20%;
    }

    .cocktail .stem{
      width:5px;
      height:30%;
      background:var(--gold);
      position:absolute;
      top:52%;
    }

    .cocktail .base{
      width:42%;
      height:5px;
      background:var(--gold);
      position:absolute;
      bottom:17%;
      border-radius:999px;
    }

    .cocktail .liquid{
      width:53%;
      height:12%;
      background:linear-gradient(90deg,#b46487,#d99358);
      opacity:.85;
      position:absolute;
      top:29%;
      clip-path:polygon(0 0,100% 0,84% 100%,16% 100%);
    }

    .cocktail .olive{
      width:22px;
      height:22px;
      border-radius:50%;
      background:#83a45e;
      position:absolute;
      top:18%;
      right:28%;
      box-shadow:0 0 0 4px rgba(131,164,94,.12);
    }

    .cocktail-label{
      position:absolute;
      bottom:24px;
      left:24px;
      right:24px;
      color:var(--muted);
      font-size:12px;
      text-align:center;
      letter-spacing:.1em;
      text-transform:uppercase;
    }

    section{
      padding:74px 0;
      border-top:1px solid rgba(255,255,255,.05);
    }

    .section-head{
      display:flex;
      align-items:flex-end;
      justify-content:space-between;
      gap:24px;
      margin-bottom:30px;
    }

    .section-number{
      color:var(--gold);
      font-size:12px;
      font-weight:800;
      letter-spacing:.16em;
      text-transform:uppercase;
      margin-bottom:6px;
    }

    h2{
      margin:0;
      font-family:Georgia,"Times New Roman",serif;
      font-size:clamp(30px,5vw,48px);
      line-height:1.15;
    }

    .section-note{
      color:var(--muted);
      max-width:520px;
      font-size:14px;
    }

    .grid-3{
      display:grid;
      grid-template-columns:repeat(3,1fr);
      gap:18px;
    }

    .grid-2{
      display:grid;
      grid-template-columns:repeat(2,1fr);
      gap:18px;
    }

    .card{
      background:linear-gradient(180deg,rgba(255,255,255,.055),rgba(255,255,255,.025));
      border:1px solid var(--line);
      border-radius:var(--radius);
      padding:24px;
      box-shadow:0 10px 35px rgba(0,0,0,.12);
    }

    .icon{
      width:44px;
      height:44px;
      border-radius:14px;
      display:grid;
      place-items:center;
      margin-bottom:16px;
      background:rgba(230,194,110,.10);
      border:1px solid rgba(230,194,110,.18);
      font-size:20px;
    }

    .card h3{
      margin:0 0 8px;
      font-size:18px;
    }

    .card p{
      margin:0;
      color:var(--muted);
      font-size:14px;
    }

    .overview{
      display:grid;
      grid-template-columns:repeat(4,1fr);
      gap:12px;
      margin-top:28px;
    }

    .overview-item{
      padding:18px;
      border-radius:16px;
      background:rgba(255,255,255,.035);
      border:1px solid var(--line);
    }

    .overview-label{
      display:block;
      color:var(--muted);
      font-size:11px;
      margin-bottom:6px;
    }

    .overview-value{
      font-weight:900;
      font-size:16px;
    }

    .steps{
      display:grid;
      gap:14px;
    }

    .step{
      display:grid;
      grid-template-columns:62px 1fr;
      gap:20px;
      align-items:start;
      padding:24px;
      border-radius:20px;
      border:1px solid var(--line);
      background:rgba(255,255,255,.035);
    }

    .step-no{
      width:52px;
      height:52px;
      border-radius:50%;
      display:grid;
      place-items:center;
      font-family:Georgia,"Times New Roman",serif;
      font-size:22px;
      font-weight:800;
      color:#17130c;
      background:linear-gradient(135deg,#f4d990,#b8852f);
    }

    .step h3{
      margin:0 0 7px;
      font-size:18px;
    }

    .step p{
      margin:0;
      color:var(--muted);
    }

    .notice{
      margin-top:18px;
      padding:18px 20px;
      border-radius:16px;
      background:rgba(230,194,110,.08);
      border:1px solid rgba(230,194,110,.22);
      color:#e9ddbf;
      font-size:14px;
    }

    details{
      border:1px solid var(--line);
      background:rgba(255,255,255,.035);
      border-radius:16px;
      padding:0 18px;
    }

    details + details{margin-top:10px}

    summary{
      cursor:pointer;
      list-style:none;
      font-weight:800;
      padding:18px 0;
    }

    summary::-webkit-details-marker{display:none}

    details p{
      color:var(--muted);
      margin:0;
      padding:0 0 18px;
    }

    .credit{
      display:grid;
      grid-template-columns:1.2fr .8fr;
      gap:18px;
    }

    .credit-box{
      border-radius:var(--radius);
      padding:28px;
      border:1px solid var(--line);
      background:rgba(255,255,255,.035);
    }

    .credit-box h3{margin-top:0}

    .credit-list{
      display:grid;
      gap:10px;
      color:var(--muted);
      font-size:14px;
    }

    .credit-list strong{color:var(--text)}

    footer{
      padding:36px 0 46px;
      text-align:center;
      color:#8f8b84;
      font-size:12px;
    }

    .pending{
      display:inline-block;
      padding:3px 8px;
      margin-left:6px;
      border-radius:999px;
      font-size:10px;
      font-weight:800;
      color:#e9d59f;
      border:1px solid rgba(230,194,110,.23);
      background:rgba(230,194,110,.06);
      vertical-align:middle;
    }

    @media (max-width:850px){
      nav{display:none}
      .hero{padding:58px 0 42px}
      .hero-grid{grid-template-columns:1fr}
      .glass-card{min-height:330px}
      .grid-3,.grid-2,.overview,.credit{grid-template-columns:1fr 1fr}
    }

    @media (max-width:560px){
      .wrap{width:min(100% - 24px,1100px)}
      .topbar-inner{min-height:60px}
      .brand{font-size:14px}
      .hero{padding-top:44px}
      h1{font-size:52px}
      .glass-card{min-height:290px;border-radius:24px}
      .grid-3,.grid-2,.overview,.credit{grid-template-columns:1fr}
      section{padding:58px 0}
      .section-head{display:block}
      .section-note{margin-top:12px}
      .step{grid-template-columns:48px 1fr;gap:14px;padding:19px}
      .step-no{width:44px;height:44px;font-size:18px}
    }
  </style>
</head>

<body>
  <header class="topbar">
    <div class="wrap topbar-inner">
      <a class="brand" href="#top">
        <span class="brand-mark">🍸</span>
        <span>おすしファクトリー</span>
      </a>

      <nav aria-label="ページ内ナビゲーション">
        <a href="#about">ゲーム概要</a>
        <a href="#contents">内容物</a>
        <a href="#setup">準備</a>
        <a href="#howto">遊び方</a>
        <a href="#faq">FAQ</a>
      </nav>
    </div>
  </header>

  <main id="top">
    <section class="hero">
      <div class="wrap hero-grid">
        <div>
          <span class="eyebrow">Official Game Manual</span>
          <h1>Cocktail<br>Party</h1>
          <div class="jp-title">公式ゲーム説明書</div>

          <p class="lead">
            騒がしいパーティーの中から、<br>
            同じカクテルを注文した相手を見つけて「乾杯！」
          </p>

          <p class="sublead">
            自分と同じカクテルを注文した人を探し出す、
            会話とひらめきのパーティーゲームです。
          </p>

          <div class="hero-actions">
            <a class="btn btn-primary" href="#howto">遊び方を見る</a>
            <a class="btn btn-secondary" href="#faq">よくある質問</a>
          </div>
        </div>

        <div class="glass-card" aria-label="カクテルグラスのイメージ">
          <div class="cocktail">
            <div class="bowl"></div>
            <div class="liquid"></div>
            <div class="stem"></div>
            <div class="base"></div>
            <div class="olive"></div>
          </div>
          <div class="cocktail-label">Find your cocktail partner.</div>
        </div>
      </div>
    </section>

    <section id="about">
      <div class="wrap">
        <div class="section-head">
          <div>
            <div class="section-number">01 / About</div>
            <h2>どんなゲーム？</h2>
          </div>
          <p class="section-note">
            同時に飛び交う会話の中から、同じカクテルを持つ相手を探すコミュニケーションゲーム。
          </p>
        </div>

        <div class="grid-3">
          <div class="card">
            <div class="icon">👂</div>
            <h3>聞き取る</h3>
            <p>周囲の会話やヒントに耳を傾け、自分と同じカクテルの相手を探します。</p>
          </div>

          <div class="card">
            <div class="icon">💬</div>
            <h3>見つける</h3>
            <p>誰が同じカクテルなのかを予想しながら、相手との距離を縮めていきます。</p>
          </div>

          <div class="card">
            <div class="icon">🥂</div>
            <h3>乾杯する</h3>
            <p>「この人だ！」と思った相手と乾杯。カクテルが一致しているか確認します。</p>
          </div>
        </div>

        <div class="overview">
          <div class="overview-item">
            <span class="overview-label">PLAYERS</span>
            <span class="overview-value">人数 <span class="pending">調整中</span></span>
          </div>
          <div class="overview-item">
            <span class="overview-label">PLAY TIME</span>
            <span class="overview-value">時間 <span class="pending">調整中</span></span>
          </div>
          <div class="overview-item">
            <span class="overview-label">AGE</span>
            <span class="overview-value">対象年齢 <span class="pending">調整中</span></span>
          </div>
          <div class="overview-item">
            <span class="overview-label">GENRE</span>
            <span class="overview-value">パーティーゲーム</span>
          </div>
        </div>
      </div>
    </section>

    <section id="contents">
      <div class="wrap">
        <div class="section-head">
          <div>
            <div class="section-number">02 / Contents</div>
            <h2>内容物</h2>
          </div>
          <p class="section-note">
            製品版の内容物に合わせて、ここにカード枚数や付属品を掲載します。
          </p>
        </div>

        <div class="grid-3">
          <div class="card">
            <div class="icon">🃏</div>
            <h3>ゲームカード</h3>
            <p>カクテルやゲーム進行に使用するカード。<span class="pending">枚数入力</span></p>
          </div>

          <div class="card">
            <div class="icon">📖</div>
            <h3>簡易説明書</h3>
            <p>ゲームの基本的な流れを確認できる、同封用の簡易説明書です。</p>
          </div>

          <div class="card">
            <div class="icon">📱</div>
            <h3>Web説明書</h3>
            <p>詳しいルールや補足事項は、この公式ページからいつでも確認できます。</p>
          </div>
        </div>
      </div>
    </section>

    <section id="setup">
      <div class="wrap">
        <div class="section-head">
          <div>
            <div class="section-number">03 / Setup</div>
            <h2>ゲームの準備</h2>
          </div>
          <p class="section-note">
            ここは最終ルールに合わせて文章を差し替えれば完成します。
          </p>
        </div>

        <div class="steps">
          <div class="step">
            <div class="step-no">1</div>
            <div>
              <h3>カードを準備する</h3>
              <p>プレイ人数に合わせて使用するカードを用意します。</p>
            </div>
          </div>

          <div class="step">
            <div class="step-no">2</div>
            <div>
              <h3>プレイヤーに配る</h3>
              <p>各プレイヤーへ必要なカードを配ります。カードの見方や公開範囲は正式ルールに合わせて記載します。</p>
            </div>
          </div>

          <div class="step">
            <div class="step-no">3</div>
            <div>
              <h3>パーティー開始！</h3>
              <p>全員の準備が整ったらゲームスタートです。</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section id="howto">
      <div class="wrap">
        <div class="section-head">
          <div>
            <div class="section-number">04 / How to Play</div>
            <h2>遊び方</h2>
          </div>
          <p class="section-note">
            まずはゲームの核になる「同じカクテルの相手を見つけて乾杯する」流れを分かりやすく掲載しています。
          </p>
        </div>

        <div class="steps">
          <div class="step">
            <div class="step-no">1</div>
            <div>
              <h3>自分のカクテルを確認</h3>
              <p>自分が担当するカクテルを確認します。</p>
            </div>
          </div>

          <div class="step">
            <div class="step-no">2</div>
            <div>
              <h3>同じカクテルの相手を探す</h3>
              <p>会話や周囲の情報を手がかりに、自分と同じカクテルを持っている相手を探します。</p>
            </div>
          </div>

          <div class="step">
            <div class="step-no">3</div>
            <div>
              <h3>「乾杯！」</h3>
              <p>同じカクテルだと思う相手を見つけたら、声をかけて乾杯します。</p>
            </div>
          </div>

          <div class="step">
            <div class="step-no">4</div>
            <div>
              <h3>結果を確認</h3>
              <p>カクテルが一致しているか確認します。一致・不一致時の処理は正式ルールに合わせて追記します。</p>
            </div>
          </div>

          <div class="step">
            <div class="step-no">5</div>
            <div>
              <h3>ゲーム終了・勝敗判定</h3>
              <p>終了条件と勝敗の決め方をここに掲載します。<span class="pending">最終ルール入力</span></p>
            </div>
          </div>
        </div>

        <div class="notice">
          <strong>制作メモ：</strong>
          現在はWebサイトのデザイン・構成を確認するための初稿です。
          確定している正式ルール、人数、プレイ時間、カード枚数などを反映すると完成版になります。
        </div>
      </div>
    </section>

    <section id="faq">
      <div class="wrap">
        <div class="section-head">
          <div>
            <div class="section-number">05 / FAQ</div>
            <h2>よくある質問</h2>
          </div>
          <p class="section-note">
            遊んでいて迷いやすい内容を、今後ここへ追加していけます。
          </p>
        </div>

        <details>
          <summary>Q. ルールの詳しい補足はどこで確認できますか？</summary>
          <p>この公式Web説明書を最新版として、補足やFAQを随時更新していく想定です。</p>
        </details>

        <details>
          <summary>Q. 同時に複数人が「乾杯！」した場合は？</summary>
          <p>正式ルールに合わせて判定方法を掲載します。</p>
        </details>

        <details>
          <summary>Q. カードを相手に見せてもいいですか？</summary>
          <p>カードの公開・非公開ルールに合わせて、ここへ掲載します。</p>
        </details>

        <details>
          <summary>Q. 説明書にないケースが発生しました。</summary>
          <p>ページ下部のお問い合わせ先よりご連絡ください。確認後、必要に応じてFAQへ追記します。</p>
        </details>
      </div>
    </section>

    <section id="credit">
      <div class="wrap">
        <div class="section-head">
          <div>
            <div class="section-number">06 / Credit</div>
            <h2>クレジット</h2>
          </div>
        </div>

        <div class="credit">
          <div class="credit-box">
            <h3>おすしファクトリー</h3>
            <div class="credit-list">
              <div><strong>制作者：</strong>おすしファクトリー</div>
              <div><strong>X：</strong>@osusi_factory</div>
              <div><strong>WEB：</strong>https://osusifactory-web.github.io/cocktail-party/</div>
            </div>
          </div>

          <div class="credit-box">
            <h3>お問い合わせ</h3>
            <p style="margin:0;color:var(--muted);font-size:14px;">
              内容物の不備やルールについてのご不明点、ご意見・ご感想などございましたら、
              お手数ですが上記よりお問い合わせください。
            </p>
          </div>
        </div>
      </div>
    </section>
  </main>

  <footer>
    <div class="wrap">
      Copyright © 2026 おすしファクトリー. All Rights Reserved.
    </div>
  </footer>
</body>
</html>
'''

path = Path("/mnt/data/cocktail-party-index.html")
path.write_text(html, encoding="utf-8")
print(f"Created: {path}")
print(f"Size: {path.stat().st_size:,} bytes")
