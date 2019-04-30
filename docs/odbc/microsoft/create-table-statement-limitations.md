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
manager: craigg
ms.openlocfilehash: f5eab1c3bf6891f10c897966035dced2ffdc10ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232215"
---
# <a name="create-table-statement-limitations"></a>CREATE TABLE 문 제한 사항
Microsoft Access, Microsoft Excel 또는 Paradoxdriver를 사용 하면 지정 되지 않은 (또는 0으로 지정 된) 텍스트 또는 이진 열의 길이, 열 길이 255로 설정 됩니다.  
  
 DBASE 드라이버를 사용 하는 경우를 지정 하지 (또는 0으로 지정 된) 텍스트 또는 이진 열의 길이, 열 길이 254로 설정 됩니다.  
  
 열이 255의 최대 지원 됩니다.  
  
 5.0은 열거나 7.0 또는 97 데이터 원본, 워크시트에 Microsoft Excel 드라이버를 사용 하는 경우 이전에 삭제 된 워크시트와 같은 이름을 사용 하 여 만들 수 없습니다. Microsoft Excel 드라이버 버전 5.0, 7.0, 또는 97 워크시트에 액세스를 사용 하는 DROP TABLE 문 워크시트 지워지지만 워크시트 이름을 삭제 하지 않습니다.  
  
 Paradox 드라이버를 사용 하는 경우 열 인덱스를 정의한 후에 테이블에 추가할 수 없습니다. CREATE TABLE 문의 인수 목록의 첫 번째 열 인덱스를 만드는 경우 인수 목록의 두 번째 열을 포함할 수 없습니다.
