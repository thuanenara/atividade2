# Atualizando especificações de SKU com API de catálogo

Em nosso Catálogo, [as especificações](https://help.vtex.com/tracks/catalog-101--5AF0XfnjfWeopIFBgs3LIQ/2NQoBv8m4Yz3oQaLgDRagP?&_ga=2.57270892.756900308.1647877394-1661745153.1646671659) são criadas no nível da categoria. Produtos e SKUs herdam suas especificações da categoria em que são colocados e todas as suas categorias pai. Isso pode causar alguma confusão ao usar nossa API para criar e atualizar SKUs.

Neste artigo, compartilhamos algumas dicas para ajudar você a atualizar uma [especificação de SKU](https://help.vtex.com/tracks/catalog-101--5AF0XfnjfWeopIFBgs3LIQ/2NQoBv8m4Yz3oQaLgDRagP?&_ga=2.103596486.756900308.1647877394-1661745153.1646671659#sku-specifications).

## SKU e sua especificação

Primeiro, você precisa selecionar um SKU e sua especificação para atualizar. Se você não souber as especificações do SKU, use o ponto de extremidade [Obter especificações do SKU](https://developers.vtex.com/vtex-rest-api/reference/catalog-api-get-sku-specification). Ele recuperará todas as especificações indexadas no SKU.

No exemplo abaixo, mostramos como seria a resposta se seu SKU tivesse duas especificações para preencher:

- Cor ( )```"FieldId": 271```
- Tamanho ( )```"FieldId": 40```

Se necessário, você poderá obter mais informações sobre cada especificação usando o ponto de extremidade [Get Specification Field](https://developers.vtex.com/vtex-rest-api/reference/catalog-api-get-specification-field).

```
Exemplo: obter especificações de SKU

[
    {
        "Id": 472,
        "SkuId": 17784,
        "FieldId": 271,
        "FieldValueId": null,
        "Text": ""
    },
    {
        "Id": 528,
        "SkuId": 17784,
        "FieldId": 40,
        "FieldValueId": 147,
        "Text": "L"
    }
]
```
>⚠️ Observe que o corpo da resposta desse endpoint é uma matriz, mas você não pode atualizar tudo de uma vez. Você pode atualizar apenas uma especificação de SKU por vez.

### Conhecendo o ```FieldValueId```

Depois de selecionar uma Especificação a ser atualizada, use o ponto de extremidade [Obter Valores de Especificações por ID de Campo](https://developers.vtex.com/vtex-rest-api/reference/catalog-api-get-specification-field-value-fieldid). Ele permite que você conheça todos os valores possíveis desta Especificação, pois você só pode atualizar a partir de uma Especificação de SKU. ```FieldValueId```

No exemplo abaixo, mostramos como seria a resposta se sua especificação tivesse três valores possíveis:

- S ( )```"FieldValueId": 144```
- M ( )```"FieldValueId": 145```
- L ( )```"FieldValueId": 146```

```
Exemplo: obter valores de especificações por ID de campo

[
    {
        "FieldValueId": 144,
        "Value": "S",
        "IsActive": true,
        "Position": 1
    },
    {
        "FieldValueId": 145,
        "Value": "M",
        "IsActive": true,
        "Position": 2
    },
    {
        "FieldValueId": 147,
        "Value": "L",
        "IsActive": true,
        "Position": 3
    }
]
```

### Atualizando a especificação de SKU ```FieldValueId```

Por fim, use o ponto de extremidade [Atualizar especificação de SKU](https://developers.vtex.com/vtex-rest-api/reference/put_api-catalog-pvt-stockkeepingunit-skuid-specification) para alterar a especificação de SKU para o novo valor desejado. ```FieldValueId```

>⚠️ As especificações de SKU só podem ter como (Combo) ou (Rádio). Você não pode alterar o campo sem atualizar o arquivo . Após esta atualização, o campo será modificado automaticamente. ```FieldType56TextFieldValueIdText```
