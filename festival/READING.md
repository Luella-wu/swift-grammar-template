# 読解ノート：自分のアプリのコード3箇所

> **氏名：** 伍夢露
> 
> **AI利用レベル：** ２
> 
> **最終更新：** 2026-10-23

生成AIに書いてもらったコードでも、自分で書いたコードでもかまいません。自分のアプリの中から3箇所を選んで、次の3つの問いに答えてください。分からないところは、生成AIに「この行は何をしていますか」「この行を消すとどうなりますか」と聞いてかまいません。ただし、書くのは自分の言葉です。

> 💡 担任の先生の指示で、項目が増えることがあります。

---

## 箇所1：（例：品名を追加するボタンの処理）

```swift
GeometryReader { geometry in
                    Image("HalloweenBackground")
                        .resizable()
                        .scaledToFill()
                        .frame(
                            width: geometry.size.width,
                            height: geometry.size.height
                        )
                        .clipped()
                }
                .ignoresSafeArea()
```

**何をしているか：**
起動画面の背景です。

**なぜこう書くのか：**
全体的に画面に表示されたいです。

**もしこう書かなかったら：**
画面のバランスが壊れるかもしれないです。

---

## 箇所2：（見出し）

```swift
                        VStack {
                            Spacer()

                            Button {
                                withAnimation(.easeOut(duration: 0.2)) {
                                    showNameInput = true
                                }
                            } label: {
                                Group {
                                    HStack(spacing: 14) {
                                        Image(systemName: "play.fill")
                                            .font(.system(size: 30, weight: .black))

                                        Text("スタート")
                                            .font(.system(size: 38, weight: .black))
                                            .lineLimit(1)
                                            .minimumScaleFactor(0.8)
                                    }
                                    .foregroundStyle(Color.deepPurple)
                                    // 固定合适宽度，使左右空间对称，并确保文字完整
                                    .frame(width: 280, height: 50)
                                    .background {
                                        Capsule()
                                            .fill(
                                                LinearGradient(
                                                    colors: [
                                                        Color.orange.opacity(0.92),
                                                        Color.yellow.opacity(0.68)
                                                    ],
                                                    startPoint: .topLeading,
                                                    endPoint: .bottomTrailing
                                                )
                                            )
                                    }
                                    .overlay {
                                        Capsule()
                                            .fill(
                                                LinearGradient(
                                                    colors: [
                                                        Color.white.opacity(0.38),
                                                        Color.clear
                                                    ],
                                                    startPoint: .top,
                                                    endPoint: .center
                                                )
                                            )
                                            .allowsHitTesting(false)
                                    }
                                    .overlay {
                                        Capsule()
                                            .stroke(
                                                LinearGradient(
                                                    colors: [
                                                        Color.yellow.opacity(0.95),
                                                        Color.orange.opacity(0.95)
                                                    ],
                                                    startPoint: .top,
                                                    endPoint: .bottom
                                                ),
                                                lineWidth: 3
                                            )
                                            .allowsHitTesting(false)
                                    }
                                    .clipShape(Capsule())
                                    .shadow(
                                        color: Color.black.opacity(0.48),
                                        radius: 12,
                                        x: 0,
                                        y: 8
                                    )
                                    .shadow(
                                        color: Color.orange.opacity(0.45),
                                        radius: 14,
                                        x: 0,
                                        y: 0
                                    )
                                    // 自动呼吸 + 手指按压放大（呼吸仅在此 Group 内生效）
                                    .scaleEffect(isStartBreathing ? 1.10 : 0.9)
                                    .animation(
                                        .easeInOut(duration: 1.6)
                                            .repeatForever(autoreverses: true),
                                        value: isStartBreathing
                                    )
                                }
                                .scaleEffect(isStartPressed ? 1.06 : 1.0)
                                .animation(
                                    .spring(response: 0.25, dampingFraction: 0.8),
                                    value: isStartPressed
                                )
                            }
                            .buttonStyle(Pressed3DButtonStyle())
                            .simultaneousGesture(
                                DragGesture(minimumDistance: 0)
                                    .onChanged { _ in
                                        if !isStartPressed {
                                            isStartPressed = true
                                        }
                                    }
                                    .onEnded { _ in
                                        isStartPressed = false
                                    }
                            )
                            .frame(maxWidth: .infinity)
                            .padding(.bottom, 150)
```

**何をしているか：**
スタート画面の「start」ボタンは、呼吸感のあるデザインに仕上げました。

**なぜこう書くのか：**
起動時にはBGMに合わせてリズムに乗ることができ、呼吸エフェクトがゲームをプレイしたいという気分を高めてくれます

**もしこう書かなかったら：**
当初のボタンのデザインは少々堅苦しかったのですが、このように変更したことで、より生き生きとした印象になりました。

---

## 箇所3：（見出し）

```swift
.navigationDestination(isPresented: $navigateToRanking) {
                    RankingView()
                }
                .navigationDestination(isPresented: $navigateToPokedex) {
                    CollectionView()
                }
```

**何をしているか：**
ボタンによって、異なる画面に移動できます

**なぜこう書くのか：**
この設定は、最も簡単でミスが起きにくい書き方です

**もしこう書かなかったら：**
他の書き方を試したことはないが、そうするとコードが非常に煩雑になり、理解しづらくなる気がする。

## 自分ではまだ説明できない箇所（正直に）

関数に関する記述の仕方がよく理解できていないので、今後の学習を通じて理解できるようになりたいと思います。
