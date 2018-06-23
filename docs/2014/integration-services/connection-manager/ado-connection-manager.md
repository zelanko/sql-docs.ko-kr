---
title: ADO 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connections [Integration Services], ADO
- connection managers [Integration Services], ADO
- ADO connection manager [Integration Services]
ms.assetid: 490418bc-5ef1-41b8-a9c8-de38aa96e0f6
caps.latest.revision: 54
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c6278b15b3e99808a015496dfa15b7b4b48b8724
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184530"
---
# <a name="ado-connection-manager"></a>ADO 연결 관리자
  ADO 연결 관리자를 사용하면 패키지에서 레코드 집합과 같은 ADO(ActiveX Data Objects) 개체에 연결할 수 있습니다. 이 연결 관리자는 일반적으로 Microsoft Visual Basic 6.0과 같은 초기 버전의 언어로 작성된 사용자 지정 태스크나 데이터 원본에 연결하기 위해 ADO를 사용하는 기존 응용 프로그램의 일부인 사용자 지정 태스크에서 사용됩니다.  
  
 패키지에 ADO 연결 관리자를 추가 하면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 런타임 시 ADO 연결으로 확인 되는 연결 관리자 속성을 설정 하 고 연결 관리자는 를추가하는관리자는연결을만들고`Connections` 패키지의 컬렉션입니다. `ConnectionManagerType` 연결 관리자의 속성이로 설정 되어 `ADO`합니다.  
  
## <a name="troubleshooting-the-ado-connection-manager"></a>ADO 연결 관리자 문제 해결  
 ADO 연결 관리자에서 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜 데이터 형식을 읽으면 다음 표에 표시된 결과가 생성됩니다.  
  
|SQL Server 데이터 형식|결과|  
|--------------------------|------------|  
|`time`, `datetimeoffset`|매개 변수가 있는 SQL 명령이 패키지에 사용되지 않을 경우 패키지가 실패합니다. 매개 변수가 있는 SQL 명령을 사용하려면 패키지에서 SQL 실행 태스크를 사용하십시오. 자세한 내용은 [SQL 실행 태스크](../control-flow/execute-sql-task.md) 및 [SQL 실행 태스크의 매개 변수 및 반환 코드](../parameters-and-return-codes-in-the-execute-sql-task.md)를 참조하세요.|  
|`datetime2`|ADO 연결 관리자가 밀리초 값을 자릅니다.|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 및 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식에 매핑하는 방법에 대한 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) 및 [Integration Services 데이터 형식](../data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="configuring-the-ado-connection-manager"></a>ADO 연결 관리자 구성  
 다음과 같은 방법으로 ADO 연결 관리자를 구성할 수 있습니다.  
  
-   선택된 공급자에 대한 요구 사항을 만족하도록 구성된 특정 연결 문자열을 제공합니다.  
  
-   공급자에 따라 연결할 데이터 원본의 이름을 포함시킵니다.  
  
-   선택된 공급자에 적합한 보안 자격 증명을 제공합니다.  
  
-   연결 관리자에서 만든 연결이 런타임에 유지될지 여부를 나타냅니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [OLE DB 연결 관리자 구성](ole-db-connection-manager.md)  
  
 연결 관리자를 프로그래밍 방식으로 구성 하는 방법에 대 한 정보를 참조 하십시오. <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../building-packages-programmatically/adding-connections-programmatically.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services &#40;SSIS&#41; 연결](integration-services-ssis-connections.md)  
  
  
