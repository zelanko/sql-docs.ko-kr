---
title: 공용 언어 런타임 (CLR) 통합에 대 한 예제 및 시나리오 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- scenarios [CLR integration]
- common language runtime [SQL Server], samples
- examples [CLR integration]
- sample applications [CLR integration]
- database objects [CLR integration], samples
- managed code [SQL Server], samples
ms.assetid: 33aac25f-abb4-4f29-af88-4a0dacd80ae7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3718a084211e7c3b2b7a14973e195a4b1c3b6b1a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62780726"
---
# <a name="usage-scenarios-and-examples-for-common-language-runtime-clr-integration"></a>CLR(공용 언어 런타임) 통합에 대한 사용 시나리오 및 예
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 CLR(공용 언어 런타임) 통합의 프로그래밍 기능을 알아보는 데 사용할 수 있는 예제 응용 프로그램, 패키지 예제 및 여러 코딩 예제가 포함되어 있습니다.  
  
 이러한 샘플 및 추가 자료를 구현 합니다. 전체 Visual Studio 프로젝트에 대 한 방문 [Microsoft SQL Server 커뮤니티 프로젝트 및 codeplex 샘플](https://go.microsoft.com/fwlink/?LinkID=193935)합니다.  
  
|이름|Description|  
|----------|-----------------|  
|[CLR UDF에서 네이티브 코드 액세스](../../../2014/database-engine/dev-guide/accessing-native-code-from-a-clr-udf.md)|데이터베이스의 어셈블리에 있는 사용자 정의 함수에서 네이티브(비관리) C++ 코드의 함수를 호출하는 방법을 보여 줍니다.|  
|[배열 매개 변수 예제](../../../2014/database-engine/dev-guide/array-parameter-sample.md)|클라이언트에서 서버의 CLR 통합 저장 프로시저로 정보 배열을 전달하여 데이터베이스에 행 집합을 만들거나 업데이트 또는 삭제하는 방법을 보여 줍니다. 이 작업은 UDT를 사용하여 수행합니다.|  
|[달력 인식 날짜 및 시간 UDT 예제](../../../2014/database-engine/dev-guide/calendar-aware-date-and-time-udt-sample.md)|달력을 사용하여 날짜와 시간을 처리할 수 있는 두 개의 UDT를 정의합니다.|  
|[CLR 트랜잭션 예제](../../../2014/database-engine/dev-guide/clr-transactions-sample.md)|System.Transactions 네임스페이스에 있는 관리되는 API를 사용하여 트랜잭션을 제어하는 방법을 보여 줍니다.|  
|[CLR 및 XML을 사용한 연락처 만들기](../../../2014/database-engine/dev-guide/contact-creation-using-clr-and-xml.md)|SQL Server의 연락처 예제는 기본 AdventureWorks2012 예제 데이터베이스의 맨 위에 추가 기능 계층을 형성하는 몇 가지 유용한 유틸리티를 제공합니다. 첫 번째 유틸리티는 AdventureWorks2012 데이터베이스와 관련이 있는 여러 부류의 사람에 대한 연락처 레코드를 만듭니다. 연락처 정보는 XML을 사용하여 지정하고 C# 기반 또는 VB 저장 프로시저로 전달되어 XML을 만들고 이 XML을 데이터베이스의 적합한 테이블에 배치합니다.|  
|[통화 형식 및 변환 함수](../../../2014/database-engine/dev-guide/currency-type-and-conversion-function.md)|C#을 사용하여 Currency 사용자 정의 데이터 형식을 정의합니다.|  
|[CLR을 사용하여 큰 개체 처리](../../../2014/database-engine/dev-guide/handling-large-objects-using-clr.md)|CLR 저장 프로시저를 사용하여 서버에서 액세스할 수 있는 파일 시스템과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 간에 LOB(Large Binary Object)를 전송하는 방법을 보여 줍니다.|  
|[Hello World Ready 예제](../../../2014/database-engine/dev-guide/hello-world-ready-sample.md)|간단한 World Ready CLR 통합 기반 저장 프로시저를 만들고, 배포 및 테스트하는 기본 작업을 보여 줍니다.|  
|[Hello World 예제](../../../2014/database-engine/dev-guide/hello-world-sample.md)|간단한 CLR 통합 기반 저장 프로시저를 만들고, 배포 및 테스트하는 기본 작업을 보여 줍니다.|  
|[In-Process 데이터 액세스 예제](../../../2014/database-engine/dev-guide/in-process-data-access-sample.md)|CLR in-process 데이터 액세스 공급자의 다양한 기능을 보여 주는 여러 간단한 함수가 포함되어 있습니다.|  
|[결과 집합 예제](../../../2014/database-engine/dev-guide/result-set-sample.md)|쿼리 결과를 읽는 동안 새 연결을 열거나 모든 결과를 메모리로 읽어 오지 않고 명령을 실행하는 방법을 보여 줍니다.|  
|[데이터 세트 보내기 예제](../../../2014/database-engine/dev-guide/send-dataset-sample.md)|서버측 CLR 기반 저장 프로시저 내에서 ADO .NET 기반 데이터 집합을 결과 집합으로 클라이언트에 반환하는 방법을 보여 줍니다.|  
|[문자열 유틸리티 함수 예제](../../../2014/database-engine/dev-guide/string-utility-functions-sample.md)|Visual C# 및 Visual Basic으로 작성되었으며 쉼표로 구분된 문자열을 열이 하나인 테이블로 분리하는 스트리밍 TVF(테이블 반환 함수)가 포함되어 있습니다.|  
|[보조 문자 인식 문자열 조작 예제](../../../2014/database-engine/dev-guide/supplementary-aware-string-manipulation-sample.md)|유니코드와 서로게이트 문자열을 모두 처리할 수 있는 5개의 보조 문자 인식 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문자열 함수의 구현 방법을 보여 줍니다.|  
|[UDT 유틸리티](../../../2014/database-engine/dev-guide/udt-utilities.md)|여러 UDT(사용자 정의 데이터 형식) 유틸리티 함수가 포함되어 있습니다.|  
|[사용하지 않는 어셈블리 정리](../../../2014/database-engine/dev-guide/unused-assembly-cleanup.md)|메타데이터 카탈로그를 쿼리하여 현재 데이터베이스에서 사용되지 않는 어셈블리를 삭제하는 .NET 저장 프로시저가 포함되어 있습니다.|  
|[사용자 정의 형식](../../../2014/database-engine/dev-guide/user-defined-type.md)|System.Data.SqlClient를 사용하는 클라이언트 응용 프로그램 및 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 간단한 UDT를 만들고 사용하는 방법을 보여 줍니다.|  
|[UTF8 문자열 사용자 정의 데이터 형식 &#40;UDT&#41;](../../../2014/database-engine/dev-guide/utf8-string-user-defined-data-type-udt.md)|UTF8로 인코딩된 값을 저장할 수 있도록 데이터베이스의 형식 시스템을 확장하는 UDT의 구현 방법을 보여 줍니다.|  
  
  
