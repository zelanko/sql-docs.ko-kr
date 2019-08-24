---
title: 추적 (Excel 용 데이터 마이닝 클라이언트) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- tracer
- connections
ms.assetid: 4aea3e17-cd0f-48dd-8f22-b54a6c716426
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 576cb395f7f488eec8ebf28ab5bc7f226cb81809
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065891"
---
# <a name="trace-data-mining-client-for-excel"></a>추적(Excel용 데이터 마이닝 클라이언트)
  ![추적 단추](media/misc-trace.gif "추적 단추")  
  
 합니다 **추적 프로그램** 대화 상자를 사용 하면 인스턴스의 전송한 문을 모니터링 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터 마이닝에 사용 됩니다. 인스턴스에 연결을 만든 후 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 클라이언트와 서버 간의 모든 상호 작용에 기록 됩니다 합니다 **추적 프로그램** 구조를 만들고, 마이닝 모델을 추가 및 확인 하는 문을 포함 하 여 창 예측 뿐만 아니라 서버에서 반환 되는 메시지입니다.  
  
 요청하는 동작에 따라 문은 DMX(Data Mining Extensions) 데이터 정의 쿼리 또는 데이터 조작 쿼리, ASSL(Analysis Services Scripting Language) 패킷 또는 Analysis Services 저장 프로시저 호출이 될 수 있습니다. 그러나 실제 숫자 결과 및 데이터 값은 표시되지 않습니다.  
  
 **추적** 의 내용과 현재 연결만 모니터링 합니다 **Tracer** 대화 상자는 저장 되지 않습니다.  
  
## <a name="options"></a>변수  
 Tracer 창  
 Excel 클라이언트에서 서버로 보내는 모든 문을 나열합니다.  
  
 요청하고 있는 동작에 따라 문은 DMX 데이터 조작 또는 데이터 정의 문, Analysis Services 저장 프로시저 호출 또는 XML/A 패킷이 될 수 있습니다.  
  
 **현재 연결**  
 현재 연결에 대한 정의를 표시하려면 클릭합니다. 이 정의에는 연결 이름, 공급자, 데이터 원본 및 카탈로그, 해당 연결이 트랜잭션에 마지막으로 사용된 시간 및 현재 상태(열려 있음, 비활성)가 포함됩니다.  
  
 **세션 모델 사용**  
 서버에서 데이터 마이닝 모델 및 구조를 임시 개체로 저장하려면 이 확인란을 선택합니다. 사용자가 만드는 모델과 구조는 현재 세션이 지속되는 동안에만 사용할 수 있습니다.  
  
 모델 또는 구조를 Analysis Services 서버에 저장하려면 이 옵션을 선택 취소합니다.  
  
 **참고** 임시 개체를 사용 하는 Excel 용 테이블 분석 도구를 사용 하는 경우에 사용할 수 있습니다. Visio용 데이터 마이닝 템플릿 및 Excel용 데이터 마이닝 클라이언트에서는 구조와 모델을 서버에 저장해야 합니다.  
  
## <a name="tracing-temporary-structures-and-models"></a>임시 구조 및 모델 추적  
 기본적으로 임시 구조 및 모델을 만드는 테이블 분석 도구를 사용하는 경우 서버와 클라이언트 간의 작업이 모니터링되지만 만든 모델이나 구조는 서버에 영구적으로 저장되지 않습니다.  
  
 테이블 분석 도구 중 하나를 사용 하는 경우 작업을 유지 하려는 경우 옵션의 선택을 수 있습니다 **세션 모델 사용**, 서버에서 영구적으로 저장할 모델을 합니다. 복사할 수도 있습니다는 **Tracer** 파일 창 회사를 나중에 만들 다시 수 있도록 합니다.  
  
## <a name="understanding-sessions"></a>세션 이해  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 연결하면 데이터 마이닝 추가 기능이 세션을 시작합니다. 각 세션은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에서 기존 세션을 식별하는 세션 식별자를 받습니다. 그러나 세션 식별자는 세션이 유효한 상태임을 보장하는 것은 아닙니다. 세션의 제한 시간이 초과되거나 세션과 관련된 연결이 해제되면 해당 세션이 만료될 수 있습니다. 세션이 만료되어 더 이상 유효하지 않으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]는 세션을 종료하고 처리 중인 모든 트랜잭션을 롤백합니다. 더 이상 유효하지 않은 세션 식별자로 전송된 메시지는 지정된 세션을 찾을 수 없다는 오류 메시지와 함께 실패합니다.  
  
 몇몇 데이터 마이닝 모델은 서버에 명시적으로 저장되지만 세션 마이닝 모델 및 구조는 그렇지 않으며 세션 데이터 마이닝 작업의 레코드는 지속되지 않습니다. 임시 마이닝 모델 및 구조는 세션을 종료하는 즉시 삭제되므로 Excel 통합 문서를 닫기 전에 보존하려는 모든 작업 내용을 저장해야 합니다.  
  
## <a name="changing-connections"></a>연결 변경  
 연결을 변경해도 이전 연결의 추적은 삭제되지 않습니다. 세션은 통합 문서를 닫아야 삭제됩니다.  
  
 에 Excel 통합 문서에서 작업 하는 동안 연결을 변경 하는 경우 연결 변경이 기록 되지 않습니다 합니다 **Tracer** 창입니다. 이름 및 현재 연결의 상태를 명시적으로 표시를 눌러야 **현재 연결**합니다.  
  
## <a name="understanding-statements-in-the-tracer"></a>Tracer의 문 이해  
 DMX는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 데이터 마이닝 모델을 만들고 작업할 때 사용할 수 있는 언어입니다. DMX를 사용하여 새 데이터 마이닝 모델의 구조를 만들고 이 모델을 학습하고 이 모델을 검색, 관리 및 예측할 수 있습니다. DMX는 DDL(데이터 정의 언어) 문, DML(데이터 조작 언어) 문, 함수 및 연산자로 구성됩니다.  
  
 DMX 문 및 해당 구문에 대한 자세한 설명은 이 항목에서 다루지 않습니다. 그러나의 정보를 사용할 수 있습니다는 **추적 프로그램** 창 DMX 문의 동작에 대 한 자세한 정보를 찾을 수 있습니다. 또한 Excel용 데이터 마이닝 추가 기능을 사용하면 손쉽게 복잡한 DMX 문을 작성하고 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서버와 상호 작용할 수 있습니다. 자세한 내용은 [쿼리 &#40;SQL Server 데이터 마이닝 추가 기능&#41;](query-sql-server-data-mining-add-ins.md)합니다.  
  
> [!NOTE]  
>  대부분의 DMX 문은 매개 변수화됩니다. 단순 유형의 경우 변수 값이 문 아래에 나열되지만 복합 유형의 경우 매개 변수 유형만 나열됩니다.  
  
 또한 SQL Server Analysis Services에서는 XMLA(XML for Analysis) 프로토콜을 사용하여 Excel용 데이터 마이닝 클라이언트 및 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스를 포함한 클라이언트 애플리케이션 간의 모든 통신을 처리합니다.  
  
 DMX 구문 및 XMLA의 명령과 요소에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 온라인 설명서를 참조하십시오.  
  
 서버로 전송하는 일부 문에 Analysis Services 시스템 저장 프로시저를 호출하는 쿼리가 포함될 수 있습니다. 자세한 내용은 SQL Server 온라인 설명서를 참조하십시오.  
  
  
