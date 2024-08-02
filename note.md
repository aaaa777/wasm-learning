# ruby.wasmについてまとめる

## 対象
ruby.wasmを全く触ったことがない人~少し触ったことがある人

## agenda

wasmの説明
wasmは純粋なアセンブリの仕様なので、乱数・現在時刻・プロセス操作などはできない（仕様に含まれていない）
それできるようにする拡張仕様がwasi
システムコール
wasi-vfsについて
どうやって実装しているのか？
https://github.com/kateinoigakukun/wasi-vfs/blob/main/src/trampoline_generated.c
const originalAddEventListener = Object.addEventListener # 元々の関数を退避
Object.addEventListener = (type, listener) => {
  console.log('event type: "' + '" is set');
  return originalAddEventListener(type, listener)
}
このようなコードをトランポリンコードという
bindgen

wit-bindgen
wit


## wasmとは

WebAssemblyのこと
Web上で動くアセンブリ言語のこと
でもやコンパイルは見せる？

アセンブリ言語とは→山崎さんのページリンク

・軌道からJSの流れまで

WASIのこと
WebAssemblyだけでは機能が足りない！
現在時刻も乱数も取れない！
wasiがある

WASIはどういう仕組み？
関数を提供する
システムコールの関数など
似たようなのにwasi-libc

wasiをリンクしてソケットなどを手に入れた！

Thats why ruby gets wasi
そのままではGemは動かない
大体のRubyのライブラリがPOSIX準拠を前提にしている

wasi-vfsについて
関数を書き換えている
bindgenのところ
addEventListenerを書き換えてしまう時に似ている
これをトランポリンコードという

