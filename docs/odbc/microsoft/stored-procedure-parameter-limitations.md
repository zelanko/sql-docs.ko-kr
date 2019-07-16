---
title: 저장 프로시저 매개 변수 제한 사항 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8b804bcf-4cce-4e6f-aa45-00bab9ef9921
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 36f1c5a18eb9f0b1939a2c3602f1ebe7695741f7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948825"
---
# <a name="stored-procedure-parameter-limitations"></a>저장 프로시저 매개 변수 제한 사항
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle을 실행 하는 저장 프로시저 10 활용 하거나 이상의 출력 매개 변수를 액세스 위반 또는 ActiveX 데이터 개체 (ADO) 오류가 발생 저장된 프로시저 호출이 실패 합니다. 8\.0.4.0.0 버전과 8.0.4.0.4의 Oracle 클라이언트 소프트웨어를 사용 하 여 Microsoft ODBC Driver for Oracle 사용 하는 경우 발생할 수 있습니다.  
  
 문제를 해결 하려면 Oracle 클라이언트 소프트웨어 8.0.4.2.0 버전으로 업그레이드 된 이상 이어야 합니다. 에 대 한 자세한 내용은 Oracle Corporation 연락처 합니다 [패치](../../odbc/microsoft/oracle-software-patches.md)합니다.  
  
> [!NOTE]  
>  Oracle 클라이언트 소프트웨어 버전 8.0.3.0.0의 초기 릴리스를 사용 하 여이 문제가 발생 하지 않습니다.
