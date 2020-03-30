---
title: BINARY BASE64 옵션 사용 | Microsoft 문서
ms.custom: ''
ms.date: 09/23/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, BINARY BASE64 option
ms.assetid: 86a7bb85-7f83-412a-b775-d2c379702fe9
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions
ms.openlocfilehash: eb192cdb9a7e9ffb43561b3b642f60144861c6df
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71199458"
---
# <a name="use-the-binary-base64-option"></a>BINARY BASE64 옵션 사용

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

쿼리에서 BINARY BASE64 옵션을 지정하면 이진 데이터가 base64 인코딩 형식으로 반환됩니다.

BINARY BASE64 옵션이 쿼리에 지정되지 않은 경우 기본적으로 AUTO 모드는 이진 데이터의 URL 인코딩을 지원합니다. 데이터베이스의 가상 루트에 대한 상대 URL에 대한 참조가 반환됩니다. 이 참조는 쿼리가 실행된 데이터베이스에 대한 참조입니다. 반환된 참조를 사용하면 후속 작업에서 실제 이진 데이터에 액세스할 수 있습니다. 이 액세스는 SQLXML ISAPI dbobject 쿼리를 사용하여 수행됩니다. 쿼리는 이미지를 식별하기 위해 정보를 충분히 제공해야 합니다. 이러한 정보에는 기본 키 열이 포함될 수 있습니다.

## <a name="column-alias"></a>열 별칭

쿼리를 볼 때와 FOR XML AUTO 모드를 사용할 때 이진 열에 별칭을 사용하지 마세요. 별칭을 사용하는 경우 별칭은 이진 데이터의 URL 인코딩으로 반환됩니다. 후속 작업에서 별칭은 의미가 없습니다. 의미 없는 별칭 및 URL 인코딩은 이미지를 검색하는 데 사용할 수 없습니다.

### <a name="cast-to-a-blob"></a>BLOB으로 캐스트

SELECT 쿼리에서 열을 BLOB(Binary Large Object)으로 캐스팅하면 해당 열은 임시 엔터티가 됩니다. BLOB은 임시이므로 연결된 테이블 이름과 열 이름은 잃게 됩니다. 시스템이 XML 계층 구조에서 이 값을 둘 위치를 알 수 없으므로, 이 캐스트로 인해 AUTO 모드 쿼리에서 오류가 발생하게 됩니다.

예를 들어, 다음 테이블의 한 행을 살펴봅니다.

```sql
CREATE TABLE MyTable (Col1 int PRIMARY KEY, Col2 binary)
INSERT INTO MyTable VALUES (1, 0x7);
```

이 쿼리에서는 BLOB(Binary Large Object)으로 캐스팅하기 때문에 오류가 발생합니다.

```sql
SELECT Col1,
CAST(Col2 as image) as Col2
FROM MyTable
FOR XML AUTO;
```

이 솔루션은 FOR XML 절에 BINARY BASE64 옵션을 추가합니다. 캐스팅을 제거하면 쿼리가 좋은 결과를 생성합니다.

```sql
SELECT Col1,
CAST(Col2 as image) as Col2
FROM MyTable
FOR XML AUTO, BINARY BASE64;
```

다음과 같은 좋은 결과가 예상됩니다.

```console
<MyTable Col1="1" Col2="Bw==" />
```

## <a name="see-also"></a>참고 항목

[FOR XML에서 AUTO 모드 사용](../../relational-databases/xml/use-auto-mode-with-for-xml.md)
