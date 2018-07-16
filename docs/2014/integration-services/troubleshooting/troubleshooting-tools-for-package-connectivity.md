---
title: 패키지 연결 문제 해결 도구 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- connectivity [Integration Services], troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: 08a019f5-8ba7-4527-97c1-e9846d4022ff
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a15f2e78fd2a3cbc88f1d3668fde27c5cdb88924
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37178080"
---
# <a name="troubleshooting-tools-package-connectivity"></a>패키지 연결 문제 해결 도구
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]는 패키지와 패키지가 데이터를 추출 및 로드하는 데이터 원본 간 연결 문제를 해결하는 데 사용할 수 있는 기능 및 도구를 제공합니다.  
  
## <a name="troubleshooting-issues-with-external-data-providers"></a>외부 데이터 공급자와의 문제 해결  
 다수의 패키지 오류가 외부 데이터 공급자와 상호 작용하는 동안 발생합니다. 하지만 이러한 공급자가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 로 반환하는 메시지에서 상호 작용 문제 해결을 시작하기에 충분한 정보를 제공하지 않는 경우가 많습니다. 이 문제 해결 요구를 다루기 위해 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 외부 데이터 원본과의 패키지 상호 작용 문제를 해결하는 데 사용할 수 있는 로깅 메시지가 포함되어 있습니다.  
  
-   **로깅을 설정하고 패키지의 Diagnostic 이벤트를 선택하여 문제 해결 메시지를 표시합니다**. 다음 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소는 외부 데이터 공급자 호출 전후에 메시지를 로그에 기록할 수 있습니다.  
  
    -   OLE DB 연결 관리자, OLE DB 원본 및 OLE DB 대상  
  
    -   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 연결 관리자 및 ADO.NET 원본  
  
    -   SQL 실행 태스크  
  
    -   조회 변환, OLE DB 명령 변환 및 느린 변경 차원 변환  
  
     로그 메시지에는 호출되는 메서드의 이름이 포함됩니다. 예를 들어 이러한 로그 메시지에 OLE DB `Open` 개체의 `Connection` 메서드나 `ExecuteNonQuery` 개체의 `Command` 메서드가 포함될 수 있습니다. 메시지의 형식은 다음과 같습니다. 여기서 '%1!s!'는 메서드 정보에 대한 자리 표시자입니다.  
  
    ```  
    ExternalRequest_pre: The object is ready to make the following external request: '%1!s!'.  
    ExternalRequest_post: '%1!s!'. The external request has completed.  
    ```  
  
     외부 데이터 공급자와의 상호 작용 문제를 해결하려면 로그를 검토하여 모든 "호출 전" 메시지(`ExternalRequest_pre`)에 해당하는 "호출 후" 메시지(`ExternalRequest_post`)가 있는지 확인합니다. 해당하는 "호출 후" 메시지가 없으면 외부 데이터 공급자가 예상대로 응답하지 않은 것을 알 수 있습니다.  
  
     다음 예에서는 이러한 로깅 메시지를 포함하는 로그의 예제 행 몇 개를 보여 줍니다.  
  
    ```  
    ExternalRequest_pre: The object is ready to make the following external request: 'ITransactionJoin::JoinTransaction'.  
    ExternalRequest_post: 'ITransactionJoin::JoinTransaction succeeded'. The external request has completed.  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.Open'.  
    ExternalRequest_post: 'IDbConnection.Open succeeded'. The external request has completed.  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.CreateCommand'.  
    ExternalRequest_post: 'IDbConnection.CreateCommand finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbCommand.ExecuteReader'.  
    ExternalRequest_post: 'IDbCommand.ExecuteReader finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDataReader.GetSchemaTable'.  
    ExternalRequest_post: 'IDataReader.GetSchemaTable finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDataReader.Close'.  
    ExternalRequest_post: 'IDataReader.Close finished'. The external request has completed."  
    ExternalRequest_pre: The object is ready to make the following external request: 'IDbConnection.Close'.  
    ExternalRequest_post: 'IDbConnection.Close finished'. The external request has completed."  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [패키지 개발용 문제 해결 도구](troubleshooting-tools-for-package-development.md)   
 [패키지 실행 문제 해결 도구](troubleshooting-tools-for-package-execution.md)  
  
  
