---
title: CREATE TABLE 문 제한 사항 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db5d2cb8decde9828acd3005551717ac9f6cef32
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096590"
---
# <a name="create-table-statement-limitations"></a>CREATE TABLE 문 제한 사항
Microsoft Access, Microsoft Excel 또는 Paradoxdriver를 사용 하 고 text 또는 binary 열의 길이를 지정 하지 않거나 0으로 지정 하면 열 길이가 255로 설정 됩니다.  
  
 DBASE 드라이버를 사용 하 고 text 또는 binary 열의 길이를 지정 하지 않거나 0으로 지정 하면 열 길이가 254로 설정 됩니다.  
  
 최대 255 열이 지원 됩니다.  
  
 Microsoft Excel 드라이버를 MicrosoftExcel 5.0, 7.0 또는 97 데이터 원본에서 사용 하는 경우 이전에 삭제 된 워크시트와 동일한 이름을 사용 하 여 워크시트를 만들 수 없습니다. Microsoft Excel 드라이버를 사용 하 여 버전 5.0, 7.0 또는 97 워크시트에 액세스할 때 DROP TABLE 문을 사용 하 여 워크시트를 지우면 워크시트 이름이 삭제 되지 않습니다.  
  
 Paradox 드라이버를 사용 하는 경우 테이블에 인덱스를 정의한 후에는 열을 추가할 수 없습니다. CREATE TABLE 문의 인수 목록에 있는 첫 번째 열이 인덱스를 만드는 경우 두 번째 열은 인수 목록에 포함할 수 없습니다.
