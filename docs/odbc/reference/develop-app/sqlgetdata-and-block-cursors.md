---
title: SQLGetData 및 블록 커서 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- SQLGetData function [ODBC], block cursors
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 12599cdc-7725-4faf-bcae-e163ea0f5851
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b60d7093552b8f1dbed87d9ad8840ddb5a9e0799
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299753"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData 및 블록 커서
**SQLGetData는** 단일 행의 단일 열에서 작동하며 여러 행의 데이터가 포함된 배열을 가져올 수 없습니다. **이는 SQLGetData의** 기본 용도가 부분적으로 긴 데이터를 가져오는 것이고 한 번에 두 개 이상의 행에 대해 이 작업을 수행할 이유가 거의 없거나 전혀 없기 때문입니다.  
  
 블록 커서와 함께 **SQLGetData를** 사용 하려면 응용 프로그램은 먼저 **SQLSetPos를** 호출 하여 단일 행에 커서를 배치합니다. 그런 다음 해당 행의 열에 대해 **SQLGetData를** 호출합니다. 그러나 이 동작은 선택 사항입니다. 드라이버가 블록 커서가 있는 **SQLGetData** 사용을 지원하는지 확인하려면 응용 프로그램이 SQL_GETDATA_EXTENSIONS 옵션을 사용하여 **SQLGetInfo를** 호출합니다.
