---
title: 실행 시 데이터 및 Text, ntext 또는 Image 열 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- data-at-execution
- ODBC data-at-execution
- image columns [ODBC]
ms.assetid: 67ffb1a6-f38d-4712-ba64-96bdd41ec2b2
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1fc35060f1584f03d75ababe76e17a030ddd8ee1
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37428592"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>실행 시 데이터 및 text, ntext 또는 image 열
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC 실행 시 데이터는 응용 프로그램에서 바인딩된 열 또는 매개 변수에 있는 대량의 데이터를 사용할 수 있도록 하는 기능입니다. 매우 큰를 검색할 때 **텍스트**를 **ntext**, 또는 **이미지** 열 응용 프로그램 못할 단순히 큰 버퍼를 할당, 버퍼로 열 바인딩 및 인출 행입니다. 매우 큰 업데이트할 때 **텍스트**를 **ntext**, 또는 **이미지** 열 응용 프로그램 못할 단순히 큰 버퍼를 할당, SQL에서 매개 변수 표식에 바인딩하지 문을 다음 문을 실행 합니다. 이러한 경우 응용 프로그램 사용 해야 합니다 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) 하거나 [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md) 해당 실행 시 데이터 옵션을 사용 하 여 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [text 및 image 열 관리](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
