---
title: 테이블 명세서 제한 사항 만들기 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE statement limitations [ODBC]
- ODBC SQL grammar, CREATE TABLE statement limitations
ms.assetid: c5067855-20c9-456f-8d63-f375b4297f2e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a83acb061cf8192dff1c6adede349f49a0b0bbdb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280874"
---
# <a name="create-table-statement-limitations"></a>CREATE TABLE 문 제한 사항
Microsoft Access, Microsoft Excel 또는 역설 드라이버를 사용하고 텍스트 또는 이진 열의 길이를 지정하지 않거나 0으로 지정하면 열 길이가 255로 설정됩니다.  
  
 dBASE 드라이버를 사용하고 텍스트 또는 이진 열의 길이가 지정되지 않았거나 0으로 지정되면 열 길이가 254로 설정됩니다.  
  
 최대 255개의 열이 지원됩니다.  
  
 Microsoft Excel 드라이버를 MicrosoftExcel 5.0, 7.0 또는 97 데이터 원본에서 사용하는 경우 이전에 삭제한 워크시트와 동일한 이름으로 워크시트를 만들 수 없습니다. Microsoft Excel 드라이버를 사용하여 버전 5.0, 7.0 또는 97 워크시트에 액세스하는 경우 DROP TABLE 문은 워크시트를 지울 수 있지만 워크시트 이름은 삭제하지 않습니다.  
  
 역설 드라이버를 사용 하는 경우 열 테이블에 인덱스를 정의 된 후에 는 열을 추가할 수 없습니다. CREATE TABLE 문의 인수 목록의 첫 번째 열이 인덱스를 만드는 경우 두 번째 열은 인수 목록에 포함할 수 없습니다.
