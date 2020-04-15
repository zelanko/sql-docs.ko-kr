---
title: 저장 프로시저 매개 변수 제한 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbd748884575791d5f170e95bc5aa465b61624b7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299203"
---
# <a name="stored-procedure-parameter-limitations"></a>저장 프로시저 매개 변수 제한 사항
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 10개 이상의 출력 매개 변수를 사용하는 Oracle 저장 프로시저를 실행하면 저장 프로시저 호출이 실패하여 액세스 위반 또는 ActiveX 데이터 개체(ADO) 오류가 발생합니다. 이는 오라클의 8.0.4.0.0 및 8.0.4.4.4 버전의 Oracle 클라이언트 소프트웨어와 함께 Microsoft ODBC 드라이버를 사용할 때 발생할 수 있습니다.  
  
 문제를 해결하려면 Oracle 클라이언트 소프트웨어를 버전 8.0.4.2.0 이상으로 업그레이드해야 합니다. [패치에](../../odbc/microsoft/oracle-software-patches.md)대한 자세한 내용은 Oracle Corporation에 문의하십시오.  
  
> [!NOTE]  
>  이 문제는 Oracle 클라이언트 소프트웨어 버전 8.0.3.0.0의 초기 릴리스에서 발생하지 않습니다.
