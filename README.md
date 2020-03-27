# openapi genaratorによるコード生成

https://github.com/OpenAPITools/openapi-generator

## open api generatorとは？
- Swagger.yamlからコードを自動生成。
- コードとは**ClientとAPI間のRequestとResponseのモデルクラス**
- 多言語対応(今回はKotlinで生成)
- brew, npm, dockerなどから実行可能(Repositoryをsubmoduleとして取り込んでも良い)

## メリット
- APIドキュメントと実際の実装に解離が起きにくくなる。
- 先にAPIドキュメントを書くことでAPIが作成される前にフロントエンドメンバーが開発できる。

## dockerによる生成

サンプルコード
```
docker run --rm -v ${PWD}:/local openapitools/openapi-generator-cli generate \
    -i https://raw.githubusercontent.com/openapitools/openapi-generator/master/modules/openapi-generator/src/test/resources/2_0/petstore.yaml \
    -g go \
    -o /local/out/go
```

```
--rm: 実行後にコンテナを自動的に削除(便利)
-v: ホスト側ディレクトリ(フルパス):コンテナ側ディレクトリ(フルパス)
-i: 使用するイメージを指定
-g: 言語指定(dockerの公式でサポートされているのか知りません)
-o: localに指定したディレクトリを作成 && 生成されたコードを設置
```

Kotlinの場合
```
docker run --rm -v ${PWD}:/local openapitools/openapi-generator-cli generate \
    -i https://raw.githubusercontent.com/openapitools/openapi-generator/master/modules/openapi-generator/src/test/resources/2_0/petstore.yaml \
    -g kotlin \
    -o /local/out/kotlin
```

petsstore.yamlの定義通りにコードが生成されます。
petsstoreはおそらくSwaggerで提供されているサンプル.yamlのようなもの。
https://petstore.swagger.io/
