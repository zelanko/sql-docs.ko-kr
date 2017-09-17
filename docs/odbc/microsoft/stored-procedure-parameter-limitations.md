---
title: "저장 프로시저 매개 변수 제한이 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8b804bcf-4cce-4e6f-aa45-00bab9ef9921
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 59beb012675e3f6af8e1aef65fe2905d353e31ab
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="stored-procedure-parameter-limitations"></a>저장된 프로시저 매개 변수의 제한
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 Oracle을 실행 하는 저장 프로시저 10을 사용 하거나 이상의 출력 매개 변수를 액세스 위반 또는 ADO ActiveX Data Objects () 오류는 저장된 프로시저 호출이 실패 합니다. 이 버전 8.0.4.0.0 그리고 8.0.4.0.4 Oracle 클라이언트 소프트웨어의 Microsoft ODBC Driver for Oracle 사용 하는 경우에 발생할 수 있습니다.  
  
 이 문제를 해결 하려면 Oracle 클라이언트 소프트웨어는 8.0.4.2.0 버전으로 업그레이드 된 이상 이어야 합니다. 에 대 한 자세한 내용은 Oracle Corporation 연락처는 [패치](../../odbc/microsoft/oracle-software-patches.md)합니다.  
  
> [!NOTE]  
>  Oracle 클라이언트 소프트웨어 버전 8.0.3.0.0 초기 릴리스에서이 문제가 발생 하지 않습니다.
