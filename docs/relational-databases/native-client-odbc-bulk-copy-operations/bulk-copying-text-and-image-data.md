---
title: 텍스트 및 이미지 데이터 대량 복사 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], text data
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], image data
- ODBC, bulk copy operations
ms.assetid: 87155bfa-3a73-4158-9d4d-cb7435dac201
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5243c862e07ad8b4f5a0b3b33ea292cecc1cb0a9
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71707905"
---
# <a name="bulk-copying-text-and-image-data"></a>텍스트 및 이미지 데이터 대량 복사
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Large **text**, **ntext**및 **image** 값은 [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md) 함수를 사용 하 여 대량 복사 됩니다. 데이터를 **bcp_moretext**와 함께 제공 한다는 것을 나타내는 *.pdata* 포인터가 NULL로 설정 된 **text**, **ntext**또는 **image** 열에 대해 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) 을 코딩 합니다. 대량 복사 된 각 행에서 각 **text**, **ntext**또는 **image** 열에 대해 제공 되는 정확한 데이터 길이를 지정 하는 것이 중요 합니다. 열에 대 한 데이터 길이가 [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)에 지정 된 열 길이와 다른 경우 [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) 를 사용 하 여 길이를 적절 한 값으로 설정 합니다. [Bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) 는 모든 비**텍스트**,**ntext**및**이미지가** 아닌 데이터를 전송 합니다. 그런 다음 **bcp_moretext** 를 호출 하 여 **text**, **ntext**또는 **image** 데이터를 별도의 단위로 보냅니다. 대량 복사 함수는 **bcp_moretext** 를 통해 전송 된 데이터의 길이가 최신 bcp_collen에 지정 된 길이와 같을 때 현재 **text**, **ntext**또는 **image** 열에 대해 모든 데이터가 전송 되었음을 확인 합니다.또는 **bcp_bind**.  
  
 **bcp_moretext** 에는 열을 식별 하는 매개 변수가 없습니다. 한 행에 **text**, **ntext**또는 **image** 열이 여러 개 있는 경우 **bcp_moretext** 는 가장 낮은 서 수 번호가 있는 열부터 시작 하 여 **text**, **ntext**또는 **image** 열에 대해 작동 합니다. 서 수 번호가 가장 높은 열로 계속 진행 합니다. **bcp_moretext** 는 전송 된 데이터의 길이가 현재 열의 최신 **bcp_collen** 또는 **bcp_bind** 에 지정 된 길이와 같을 때 한 열에서 다음 열로 이동 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 대량 복사 작업 &#40;수행&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
