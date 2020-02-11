---
title: SQLTransact (Access 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f4d4b3d8d417591bd72dde22240c81a91d80f990
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948978"
---
# <a name="sqltransact-access-driver"></a>SQLTransact(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 드라이버 관련 정보에 대 한 액세스를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 Microsoft Access 드라이버를 사용 하는 경우 **Sqltransact**호출에서 *fType* 인수에 대해 SQL_COMMIT 및 SQL_ROLLBACK 지원 됩니다.  
  
 커밋 프로세스 중에 오류가 발생 하는 경우 Microsoft Access 드라이버 설정의 데이터베이스 복구 옵션을 사용 하거나 **SQLConfigDataSource** 함수에서 REPAIR_DB 키워드를 사용 하 여 영향을 받는 데이터베이스를 복구할 수 있습니다.
