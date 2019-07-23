---
title: ADO 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], ADO
- connection managers [Integration Services], ADO
- ADO connection manager [Integration Services]
ms.assetid: 490418bc-5ef1-41b8-a9c8-de38aa96e0f6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 920885c27d849ac49dc5e6c801a432ccdb493e77
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898836"
---
# <a name="ado-connection-manager"></a>ADO 연결 관리자

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ADO 연결 관리자를 사용하면 패키지에서 레코드 집합과 같은 ADO(ActiveX Data Objects) 개체에 연결할 수 있습니다. 이 연결 관리자는 일반적으로 Microsoft Visual Basic 6.0과 같은 초기 버전의 언어로 작성된 사용자 지정 태스크나 데이터 원본에 연결하기 위해 ADO를 사용하는 기존 애플리케이션의 일부인 사용자 지정 태스크에서 사용됩니다.  
  
 패키지에 ADO 연결 관리자를 추가하면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 런타임에 ADO 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하고, 연결 관리자를 패키지의 **Connections** 컬렉션에 추가합니다. 연결 관리자의 **ConnectionManagerType** 속성이 **ADO**로 설정됩니다.  
  
## <a name="troubleshooting-the-ado-connection-manager"></a>ADO 연결 관리자 문제 해결  
 ADO 연결 관리자에서 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜 데이터 형식을 읽으면 다음 표에 표시된 결과가 생성됩니다.  
  
|SQL Server 데이터 형식|결과|  
|--------------------------|------------|  
|**time**, **datetimeoffset**|매개 변수가 있는 SQL 명령이 패키지에 사용되지 않을 경우 패키지가 실패합니다. 매개 변수가 있는 SQL 명령을 사용하려면 패키지에서 SQL 실행 태스크를 사용하십시오. 자세한 내용은 [SQL 실행 태스크](../../integration-services/control-flow/execute-sql-task.md) 및 [SQL 실행 태스크의 매개 변수 및 반환 코드](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663)를 참조하세요.|  
|**datetime2**|ADO 연결 관리자가 밀리초 값을 자릅니다.|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 및 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식에 매핑하는 방법에 대한 자세한 내용은 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) 및 [Integration Services 데이터 형식](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="configuring-the-ado-connection-manager"></a>ADO 연결 관리자 구성  
 다음과 같은 방법으로 ADO 연결 관리자를 구성할 수 있습니다.  
  
-   선택된 공급자에 대한 요구 사항을 만족하도록 구성된 특정 연결 문자열을 제공합니다.  
  
-   공급자에 따라 연결할 데이터 원본의 이름을 포함시킵니다.  
  
-   선택된 공급자에 적합한 보안 자격 증명을 제공합니다.  
  
-   연결 관리자에서 만든 연결이 런타임에 유지될지 여부를 나타냅니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [OLE DB 연결 관리자 구성](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 연결](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
