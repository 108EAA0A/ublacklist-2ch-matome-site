# ublacklist-2ch-matome-site

2ch転載系のまとめサイトの一覧としてニコニコ大百科の記事が有用だったので、そこからスクレイピングして一覧を出力したものが置いてある

## deploy

chromium系ブラウザのconsoleで以下を実行し、結果を手動でtxtに保存してメンテしている

そのうち自動化したい

```js
const format = (a) => {
	if (!a) return []
	const link = a.href.replace(/https?:\/\//, '*://').replace('://www.', '://*.').replace(/index\.(html|php)$/, '')
	return [link.endsWith('/') ? link + '*' : link + '/*']
}
// for https://dic.nicovideo.jp/a/2ch%E9%96%A2%E9%80%A3%E3%81%BE%E3%81%A8%E3%82%81%E3%82%B5%E3%82%A4%E3%83%88%E3%81%AE%E4%B8%80%E8%A6%A7
console.log($$('#article > table > tbody > tr > td:first-of-type  > a:last-of-type[target="_blank"][rel="nofollow"]').flatMap(format).sort().join('\n'))
// for https://dic.nicovideo.jp/a/%E6%9C%AA%E7%99%BB%E9%8C%B22ch%E9%96%A2%E9%80%A3%E3%81%BE%E3%81%A8%E3%82%81%E3%82%B5%E3%82%A4%E3%83%88%E3%81%AE%E4%B8%80%E8%A6%A7
console.log($$('#article > table > tbody > tr > td:nth-of-type(2) > a:last-of-type[target="_blank"][rel="nofollow"]').flatMap(format).sort().join('\n'))
```
