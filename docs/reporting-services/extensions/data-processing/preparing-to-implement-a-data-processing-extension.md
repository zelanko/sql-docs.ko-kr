---
title: "데이터 처리 확장 프로그램 구현 준비 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- interfaces [Reporting Services]
- data processing extensions [Reporting Services], implementing
ms.assetid: 698817e4-33da-4eb5-9407-4103e1c35247
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 6d516201d8018b1d58b77be8e3cf543745da037a
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="preparing-to-implement-a-data-processing-extension"></a>데이터 처리 확장 프로그램 구현 준비
  구현 하기 전에 프로그램 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램을 구현할 인터페이스를 정의 해야 합니다. 인터페이스의 전체 집합의 확장 프로그램별 구현을 제공 하려는 경우 또는 같은 하위 집합에 대 한 구현 초점을 원할 수 있습니다는 <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> 및 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand> 는 클라이언트는 결과 집합을 주로 상호 작용 하는 인터페이스는 **DataReader** 개체를 사용 하 여 프로그램 [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] 결과 집합 및 데이터 원본 사이의 연결 고리로 데이터 처리 확장 프로그램입니다.  
  
 다음 두 가지 방법 중 하나로 데이터 처리 확장 프로그램을 구현할 수 있습니다.  
  
-   데이터 처리 확장 프로그램 클래스를 구현할 수는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 데이터 공급자 인터페이스에서 제공 된 데이터 처리 확장 프로그램 인터페이스 및 필요에 따라 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]합니다.  
  
-   데이터 처리 확장 프로그램 클래스는 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]에서 제공하는 데이터 처리 확장 프로그램 인터페이스 및 확장된 데이터 처리 확장 프로그램 인터페이스(선택 사항)를 구현할 수 있습니다.  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램에서 특정 속성 또는 메서드를 지원하지 않을 경우 속성 또는 메서드를 작업 없음으로 구현합니다. 클라이언트에서 특정 동작을 기대 하는 경우에 throw 된 **NotSupportedException** 예외입니다.  
  
> [!NOTE]  
>  속성 또는 메서드에 대한 작업 없음 구현은 구현 대상으로 선택한 인터페이스의 속성 및 메서드에만 적용됩니다. 구현하지 않도록 선택한 인터페이스는 데이터 처리 확장 프로그램 어셈블리에 포함되지 않아야 합니다. 인터페이스가 필수인지 아니면 선택적인지에 대한 자세한 내용은 이 섹션의 후반에 나오는 표를 참조하십시오.  
  
## <a name="required-extension-functionality"></a>필수 확장 프로그램 기능  
 각 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램은 다음 기능을 제공해야 합니다.  
  
-   데이터 원본에 연결합니다.  
  
-   쿼리를 분석하고 결과 집합에 대한 필드 이름 목록을 반환합니다.  
  
-   데이터 원본에 대한 쿼리를 실행하고 행 집합을 반환합니다.  
  
-   단일 값 매개 변수를 쿼리에 전달합니다.  
  
-   행 집합의 행을 반복 처리하고 데이터를 검색합니다.  
  
 각 데이터 처리 확장 프로그램은 다음 기능을 포함하도록 확장할 수 있습니다.  
  
-   쿼리를 분석하고 쿼리에 사용된 매개 변수 이름 목록을 반환합니다.  
  
-   쿼리를 분석하고 쿼리 그룹화 기준이 되는 필드 목록을 반환합니다.  
  
-   쿼리를 분석하고 쿼리 정렬 기준이 되는 필드 목록을 반환합니다.  
  
-   연결 문자열에 독립적인 데이터 원본에 연결하기 위한 사용자 이름과 암호를 제공합니다.  
  
-   행 집합의 행을 반복 처리하고 데이터 값에 대한 보조 메타데이터를 검색합니다.  
  
-   서버에서 데이터를 집계합니다.  
  
## <a name="available-extension-interfaces"></a>사용 가능한 확장 프로그램 인터페이스  
 다음 표에서는 사용 가능한 인터페이스를 보여 주고 구현이 필수인지 선택적인지 설명합니다.  
  
|인터페이스|Description|구현|  
|---------------|-----------------|--------------------|  
|IDbConnection|데이터 원본의 고유 세션을 나타냅니다. 클라이언트/서버 데이터베이스 시스템의 경우에는 세션이 서버에 대한 네트워크 연결과 같을 수 있습니다.|필수임|  
|IDbConnectionExtension|보안 및 인증과 관련하여 [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] 데이터 처리 확장 프로그램으로 구현할 수 있는 추가 연결 속성을 나타냅니다.|선택 사항|  
|IDbTransaction|로컬 트랜잭션을 나타냅니다.|필수임|  
|IDbTransactionExtension|[!INCLUDE[ssRS](../../../includes/ssrs-md.md)] 데이터 처리 확장 프로그램으로 구현할 수 있는 추가 트랜잭션 속성을 나타냅니다.|선택 사항|  
|IDbCommand|데이터 원본에 연결되었을 때 사용되는 쿼리 또는 명령을 나타냅니다.|필수임|  
|IDbCommandAnalysis|쿼리를 분석하고 쿼리에서 사용된 매개 변수 이름 목록을 반환하기 위한 추가 명령 정보를 나타냅니다.|선택 사항|  
|IDataParameter|명령 또는 쿼리에 전달된 매개 변수 또는 이름/값 쌍을 나타냅니다.|필수임|  
|IDataParameterCollection|명령 또는 쿼리와 관련된 모든 매개 변수의 모음을 나타냅니다.|필수임|  
|IDataReader|데이터 원본에서 데이터의 정방향 전용, 읽기 전용 스트림을 읽는 방법을 제공합니다.|필수임|  
|IDataReaderExtension|데이터 원본에서 명령을 실행하여 얻은 정방향 전용 결과 집합 스트림을 하나 이상 읽는 방법을 제공합니다. 이 인터페이스는 필드 집계에 대한 추가 지원을 제공합니다.|선택 사항|  
|IExtension|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램에 대한 기본 클래스를 제공합니다. 또한 구현 전문가는 이 인터페이스를 사용하여 확장 프로그램에 대한 지역화된 이름을 포함시키고 구성 파일에서 확장 프로그램으로 구성 설정을 전달할 수 있습니다.|필수임|  
  
 데이터 처리 확장 프로그램 인터페이스는 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 데이터 공급자 인터페이스, 메서드 및 속성의 하위 집합과 동일합니다(가능한 경우 항상). 전체 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 데이터 공급자를 구현하는 방법은 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK(소프트웨어 개발 키트) 설명서의 ".NET Framework 데이터 공급자 구현(Implementing a .NET Framework Data Provider)"을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [Reporting Services 확장 프로그램](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [데이터 처리 확장 프로그램 구현](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 확장 프로그램 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
