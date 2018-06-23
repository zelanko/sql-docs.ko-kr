---
title: Progress Reports 데이터 열 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Progress Reports event category
ms.assetid: d34a6322-e26b-4454-b98f-32307d6956b5
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8679a1e432402af28a36fa6ccfddac7f19fcf96c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172990"
---
# <a name="progress-reports-data-columns"></a>Progress Reports 데이터 열
  Progress Reports 이벤트 범주에는 다음과 같은 이벤트 클래스가 있습니다.  
  
|**이벤트 ID**|**이벤트 이름**|**이벤트 설명**|  
|------------------|--------------------|---------------------------|  
|5|Progress Report Begin|진행률 보고서가 시작되었습니다.|  
|6|Progress Report End|진행률 보고서가 종료되었습니다.|  
|7|Progress Report Current|진행률 보고서가 현재 처리되고 있습니다.|  
|8|Progress Report Error|진행률 보고서 오류입니다.|  
  
 다음 표에서는 이러한 각 이벤트 클래스에 대한 데이터 열을 나열합니다.  
  
## <a name="progress-report-begindata-columns"></a>Progress Report Begin - 데이터 열  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1|1|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 1: 프로세스<br /><br /> 2: 병합<br /><br /> 3: 삭제<br /><br /> 4: DeleteOldAggregations<br /><br /> 5: 다시 작성<br /><br /> 6: 커밋<br /><br /> 7: 롤백<br /><br /> 8: CreateIndexes<br /><br /> 9: CreateTable<br /><br /> 10: InsertInto<br /><br /> 11: 트랜잭션<br /><br /> 12: 초기화<br /><br /> 13: 불연속화<br /><br /> 14: 쿼리<br /><br /> 15: CreateView<br /><br /> 16: WriteData<br /><br /> 17: ReadData<br /><br /> 18: GroupData<br /><br /> 19: GroupDataRecord<br /><br /> 20: BuildIndex<br /><br /> 21: 집계<br /><br /> 22: BuildDecode<br /><br /> 23: WriteDecode<br /><br /> 24: BuildDMDecode<br /><br /> 25: ExecuteSQL<br /><br /> 26: ExecuteModifiedSQL<br /><br /> 27: 연결<br /><br /> 28: BuildAggsAndIndexes<br /><br /> 29: MergeAggsOnDisk<br /><br /> 30: BuildIndexForRigidAggs<br /><br /> 31: BuildIndexForFlexibleAggs<br /><br /> 32: WriteAggsAndIndexes<br /><br /> 33: WriteSegment<br /><br /> 34: DataMiningProgress<br /><br /> 35: ReadBufferFullReport<br /><br /> 36: ProactiveCacheConversion<br /><br /> 37: 백업<br /><br /> 38: 복원<br /><br /> 39: 동기화<br /><br /> 40: 처리 일정<br /><br /> 41: 분리<br /><br /> 42: 연결<br /><br /> 43: Analyze\Encode 데이터<br /><br /> 44: 세그먼트를 압축 합니다.<br /><br /> 45: 테이블 열 작성<br /><br /> 46: 관계 빌드 준비<br /><br /> 47: 관계 세그먼트 빌드<br /><br /> 48: 부하<br /><br /> 49: 메타 데이터 로드<br /><br /> 50: 데이터 로드<br /><br /> 51: 부하를 게시 합니다.<br /><br /> 52: 백업 하는 동안 메타 데이터 탐색<br /><br /> 53: VertiPaq<br /><br /> 54: 계층 처리<br /><br /> 55: 스위칭 사전|  
|CurrentTime|2|5|보고된 이벤트의 현재 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|이벤트가 시작된 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|JobID|7|1|보고된 이벤트와 연결된 작업 ID를 포함합니다.|  
|SessionType|8|8|보고된 이벤트와 연결된 세션 유형(이벤트를 발생시키는 엔터티)을 포함합니다. 처리 중인 이벤트의 경우 값은 다음과 같습니다.<br /><br /> 1 = 사용자<br /><br /> 2 = 자동 관리 캐싱<br /><br /> 3 = 지연 처리|  
|ObjectID|11|8|보고된 이벤트와 연결된 개체 ID(문자열)를 포함합니다.|  
|ObjectType|12|1|개체 유형을 포함합니다.|  
|ObjectName|13|8|보고된 이벤트와 연결된 개체의 이름을 포함합니다.|  
|ObjectPath|14|8|보고된 이벤트와 연결된 개체의 개체 경로를 해당 개체의 부모로 시작하는 부모 목록(쉼표로 구분)으로 포함합니다.|  
|ObjectReference|15|8|모든 부모에 대해 XML로 인코딩되고 개체를 설명하는 태그를 사용하는 보고된 이벤트에 대한 개체 참조를 포함합니다.|  
|ConnectionID|25|1|보고된 이벤트와 연결된 고유 연결 ID를 포함합니다.|  
|DatabaseName|28|8|보고된 이벤트가 발생한 데이터베이스의 이름을 포함합니다.|  
|NTUserName|32|8|보고된 이벤트와 연결된 Windows 사용자 계정을 포함합니다.|  
|NTDomainName|33|8|보고된 이벤트와 연결된 Windows 도메인 계정을 포함합니다.|  
|SessionID|39|8|보고된 이벤트와 연결된 세션 ID를 포함합니다.|  
|NTCanonicalUserName|40|8|정식 사용자 이름(예: engineering.microsoft.com/software/someone)입니다.|  
|SPID|41|1|보고된 이벤트와 연결된 사용자 세션을 고유하게 식별하는 SPID(서버 프로세스 ID)를 포함합니다. SPID는 XMLA(XML for Analysis)에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|보고된 이벤트와 연결된 텍스트 데이터를 포함합니다.|  
|데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면|43|8|보고된 이벤트가 발생한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 포함합니다.|  
  
## <a name="progress-report-enddata-columns"></a>Progress Report End - 데이터 열  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1|1|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 1: 프로세스<br /><br /> 2: 병합<br /><br /> 3: 삭제<br /><br /> 4: DeleteOldAggregations<br /><br /> 5: 다시 작성<br /><br /> 6: 커밋<br /><br /> 7: 롤백<br /><br /> 8: CreateIndexes<br /><br /> 9: CreateTable<br /><br /> 10: InsertInto<br /><br /> 11: 트랜잭션<br /><br /> 12: 초기화<br /><br /> 13: 불연속화<br /><br /> 14: 쿼리<br /><br /> 15: CreateView<br /><br /> 16: WriteData<br /><br /> 17: ReadData<br /><br /> 18: GroupData<br /><br /> 19: GroupDataRecord<br /><br /> 20: BuildIndex<br /><br /> 21: 집계<br /><br /> 22: BuildDecode<br /><br /> 23: WriteDecode<br /><br /> 24: BuildDMDecode<br /><br /> 25: ExecuteSQL<br /><br /> 26: ExecuteModifiedSQL<br /><br /> 27: 연결<br /><br /> 28: BuildAggsAndIndexes<br /><br /> 29: MergeAggsOnDisk<br /><br /> 30: BuildIndexForRigidAggs<br /><br /> 31: BuildIndexForFlexibleAggs<br /><br /> 32: WriteAggsAndIndexes<br /><br /> 33: WriteSegment<br /><br /> 34: DataMiningProgress<br /><br /> 35: ReadBufferFullReport<br /><br /> 36: ProactiveCacheConversion<br /><br /> 37: 백업<br /><br /> 38: 복원<br /><br /> 39: 동기화<br /><br /> 40: 처리 일정<br /><br /> 41: 분리<br /><br /> 42: 연결<br /><br /> 43: Analyze\Encode 데이터<br /><br /> 44: 세그먼트를 압축 합니다.<br /><br /> 45: 테이블 열 작성<br /><br /> 46: 관계 빌드 준비<br /><br /> 47: 관계 세그먼트 빌드<br /><br /> 48: 부하<br /><br /> 49: 메타 데이터 로드<br /><br /> 50: 데이터 로드<br /><br /> 51: 부하를 게시 합니다.<br /><br /> 52: 백업 하는 동안 메타 데이터 탐색<br /><br /> 53: VertiPaq<br /><br /> 54: 계층 처리<br /><br /> 55: 스위칭 사전|  
|CurrentTime|2|5|보고된 이벤트의 현재 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|이벤트가 시작된 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간을 포함합니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|Duration|5|2|이벤트에 의해 사용된 경과 시간(밀리초)을 포함합니다.|  
|CPUTime|6|2|이벤트에 의해 사용된 CPU 시간(밀리초)을 포함합니다.|  
|JobID|7|1|보고된 이벤트와 연결된 작업 ID를 포함합니다.|  
|SessionType|8|8|보고된 이벤트와 연결된 세션 유형(이벤트를 발생시키는 엔터티)을 포함합니다. 처리 중인 이벤트의 경우 값은 다음과 같습니다.<br /><br /> 1 = 사용자<br /><br /> 2 = 자동 관리 캐싱<br /><br /> 3 = 지연 처리|  
|ProgressTotal|9|1|보고된 이벤트의 총 진행률을 포함합니다.|  
|IntegerData|10|1|처리 중인 이벤트에 대해 현재 처리된 행 개수와 같이 보고된 이벤트와 연결된 정수 데이터를 포함합니다.|  
|ObjectID|11|8|보고된 이벤트와 연결된 개체 ID(문자열)를 포함합니다.|  
|ObjectType|12|1|개체 유형을 포함합니다.|  
|ObjectName|13|8|보고된 이벤트와 연결된 개체의 이름을 포함합니다.|  
|ObjectPath|14|8|보고된 이벤트와 연결된 개체의 개체 경로를 해당 개체의 부모로 시작하는 부모 목록(쉼표로 구분)으로 포함합니다.|  
|ObjectReference|15|8|모든 부모에 대해 XML로 인코딩되고 개체를 설명하는 태그를 사용하는 보고된 이벤트에 대한 개체 참조를 포함합니다.|  
|Severity|22|1|보고된 이벤트와 연결된 예외의 심각도 수준을 포함합니다. 값은 다음과 같습니다.<br /><br /> 0 = 성공<br /><br /> 1 = 알림<br /><br /> 2 = 경고<br /><br /> 3 = 오류|  
|성공|23|1|보고된 서버 이벤트의 성공 또는 실패를 포함합니다. 값은 다음과 같습니다.<br /><br /> 0 = 실패<br /><br /> 1 = 성공|  
|Error|24|1|지정된 이벤트의 오류 번호를 포함합니다.|  
|ConnectionID|25|1|보고된 이벤트와 연결된 고유 연결 ID를 포함합니다.|  
|DatabaseName|28|8|보고된 이벤트가 발생한 데이터베이스의 이름을 포함합니다.|  
|NTUserName|32|8|보고된 이벤트와 연결된 Windows 사용자 계정을 포함합니다.|  
|NTDomainName|33|8|보고된 이벤트와 연결된 Windows 도메인 계정을 포함합니다.|  
|SessionID|39|8|보고된 이벤트와 연결된 세션 ID를 포함합니다.|  
|NTCanonicalUserName|40|8|보고된 이벤트와 연결된 Windows 사용자 이름을 포함합니다. 이는 정식 사용자 이름으로 engineering.microsoft.com/software/user와 같습니다.|  
|SPID|41|1|보고된 이벤트와 연결된 사용자 세션을 고유하게 식별하는 SPID(서버 프로세스 ID)를 포함합니다. SPID는 XMLA(XML for Analysis)에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|보고된 이벤트와 연결된 텍스트 데이터를 포함합니다.|  
|데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면|43|8|보고된 이벤트가 발생한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 포함합니다.|  
  
## <a name="progress-report-currentdata-columns"></a>Progress Report Current - 데이터 열  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1|1|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 1: 프로세스<br /><br /> 2: 병합<br /><br /> 3: 삭제<br /><br /> 4: DeleteOldAggregations<br /><br /> 5: 다시 작성<br /><br /> 6: 커밋<br /><br /> 7: 롤백<br /><br /> 8: CreateIndexes<br /><br /> 9: CreateTable<br /><br /> 10: InsertInto<br /><br /> 11: 트랜잭션<br /><br /> 12: 초기화<br /><br /> 13: 불연속화<br /><br /> 14: 쿼리<br /><br /> 15: CreateView<br /><br /> 16: WriteData<br /><br /> 17: ReadData<br /><br /> 18: GroupData<br /><br /> 19: GroupDataRecord<br /><br /> 20: BuildIndex<br /><br /> 21: 집계<br /><br /> 22: BuildDecode<br /><br /> 23: WriteDecode<br /><br /> 24: BuildDMDecode<br /><br /> 25: ExecuteSQL<br /><br /> 26: ExecuteModifiedSQL<br /><br /> 27: 연결<br /><br /> 28: BuildAggsAndIndexes<br /><br /> 29: MergeAggsOnDisk<br /><br /> 30: BuildIndexForRigidAggs<br /><br /> 31: BuildIndexForFlexibleAggs<br /><br /> 32: WriteAggsAndIndexes<br /><br /> 33: WriteSegment<br /><br /> 34: DataMiningProgress<br /><br /> 35: ReadBufferFullReport<br /><br /> 36: ProactiveCacheConversion<br /><br /> 37: 백업<br /><br /> 38: 복원<br /><br /> 39: 동기화<br /><br /> 40: 처리 일정<br /><br /> 41: 분리<br /><br /> 42: 연결<br /><br /> 43: Analyze\Encode 데이터<br /><br /> 44: 세그먼트를 압축 합니다.<br /><br /> 45: 테이블 열 작성<br /><br /> 46: 관계 빌드 준비<br /><br /> 47: 관계 세그먼트 빌드<br /><br /> 48: 부하<br /><br /> 49: 메타 데이터 로드<br /><br /> 50: 데이터 로드<br /><br /> 51: 부하를 게시 합니다.<br /><br /> 52: 백업 하는 동안 메타 데이터 탐색<br /><br /> 53: VertiPaq<br /><br /> 54: 계층 처리<br /><br /> 55: 스위칭 사전|  
|CurrentTime|2|5|보고된 이벤트의 현재 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|이벤트가 시작된 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|JobID|7|1|보고된 이벤트와 연결된 작업 ID를 포함합니다.|  
|SessionType|8|8|보고된 이벤트와 연결된 세션 유형(이벤트를 발생시키는 엔터티)을 포함합니다. 처리 중인 이벤트의 경우 값은 다음과 같습니다.<br /><br /> 1 = 사용자<br /><br /> 2 = 자동 관리 캐싱<br /><br /> 3 = 지연 처리|  
|ProgressTotal|9|1|보고된 이벤트의 총 진행률을 포함합니다.|  
|IntegerData|10|1|처리 중인 이벤트에 대해 현재 처리된 행 개수와 같이 보고된 이벤트와 연결된 정수 데이터를 포함합니다.|  
|ObjectID|11|8|보고된 이벤트와 연결된 개체 ID(문자열)를 포함합니다.|  
|ObjectType|12|1|개체 유형을 포함합니다.|  
|ObjectName|13|8|보고된 이벤트와 연결된 개체의 이름을 포함합니다.|  
|ObjectPath|14|8|보고된 이벤트와 연결된 개체의 개체 경로를 해당 개체의 부모로 시작하는 부모 목록(쉼표로 구분)으로 포함합니다.|  
|ObjectReference|15|8|모든 부모에 대해 XML로 인코딩되고 개체를 설명하는 태그를 사용하는 보고된 이벤트에 대한 개체 참조를 포함합니다.|  
|ConnectionID|25|1|보고된 이벤트와 연결된 고유 연결 ID를 포함합니다.|  
|DatabaseName|28|8|보고된 이벤트가 발생한 데이터베이스의 이름을 포함합니다.|  
|SessionID|39|8|보고된 이벤트와 연결된 세션 ID를 포함합니다.|  
|SPID|41|1|보고된 이벤트와 연결된 사용자 세션을 고유하게 식별하는 SPID(서버 프로세스 ID)를 포함합니다. SPID는 XMLA(XML for Analysis)에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|보고된 이벤트와 연결된 텍스트 데이터를 포함합니다.|  
|데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면|43|8|보고된 이벤트가 발생한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 포함합니다.|  
  
## <a name="progress-report-errordata-columns"></a>Progress Report Error - 데이터 열  
  
|**열 이름**|**열 ID**|**열 유형**|**열 설명**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|이벤트 클래스는 이벤트를 분류하는 데 사용됩니다.|  
|EventSubclass|1|1|이벤트 하위 클래스는 각 이벤트 클래스에 대한 추가 정보를 제공합니다.<br /><br /> 1: 프로세스<br /><br /> 2: 병합<br /><br /> 3: 삭제<br /><br /> 4: DeleteOldAggregations<br /><br /> 5: 다시 작성<br /><br /> 6: 커밋<br /><br /> 7: 롤백<br /><br /> 8: CreateIndexes<br /><br /> 9: CreateTable<br /><br /> 10: InsertInto<br /><br /> 11: 트랜잭션<br /><br /> 12: 초기화<br /><br /> 13: 불연속화<br /><br /> 14: 쿼리<br /><br /> 15: CreateView<br /><br /> 16: WriteData<br /><br /> 17: ReadData<br /><br /> 18: GroupData<br /><br /> 19: GroupDataRecord<br /><br /> 20: BuildIndex<br /><br /> 21: 집계<br /><br /> 22: BuildDecode<br /><br /> 23: WriteDecode<br /><br /> 24: BuildDMDecode<br /><br /> 25: ExecuteSQL<br /><br /> 26: ExecuteModifiedSQL<br /><br /> 27: 연결<br /><br /> 28: BuildAggsAndIndexes<br /><br /> 29: MergeAggsOnDisk<br /><br /> 30: BuildIndexForRigidAggs<br /><br /> 31: BuildIndexForFlexibleAggs<br /><br /> 32: WriteAggsAndIndexes<br /><br /> 33: WriteSegment<br /><br /> 34: DataMiningProgress<br /><br /> 35: ReadBufferFullReport<br /><br /> 36: ProactiveCacheConversion<br /><br /> 37: 백업<br /><br /> 38: 복원<br /><br /> 39: 동기화<br /><br /> 40: 처리 일정<br /><br /> 41: 분리<br /><br /> 42: 연결<br /><br /> 43: Analyze\Encode 데이터<br /><br /> 44: 세그먼트를 압축 합니다.<br /><br /> 45: 테이블 열 작성<br /><br /> 46: 관계 빌드 준비<br /><br /> 47: 관계 세그먼트 빌드<br /><br /> 48: 부하<br /><br /> 49: 메타 데이터 로드<br /><br /> 50: 데이터 로드<br /><br /> 51: 부하를 게시 합니다.<br /><br /> 52: 백업 하는 동안 메타 데이터 탐색<br /><br /> 53: VertiPaq<br /><br /> 54: 계층 처리<br /><br /> 55: 스위칭 사전|  
|CurrentTime|2|5|보고된 이벤트의 현재 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|StartTime|3|5|이벤트가 시작된 시간을 포함합니다(사용 가능한 경우). 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|EndTime|4|5|이벤트가 종료된 시간을 포함합니다. 이 열은 SQL:BatchStarting 또는 SP:Starting과 같은 시작하는 이벤트 클래스의 경우 채워지지 않습니다. 필터링 형식은 'YYYY-MM-DD' 및 'YYYY-MM-DD HH:MM:SS'입니다.|  
|Duration|5|2|이벤트에 의해 사용된 경과 시간(밀리초)을 포함합니다.|  
|JobID|7|1|보고된 이벤트와 연결된 작업 ID를 포함합니다.|  
|SessionType|8|8|보고된 이벤트와 연결된 세션 유형(이벤트를 발생시키는 엔터티)을 포함합니다. 처리 중인 이벤트의 경우 값은 다음과 같습니다.<br /><br /> 1 = 사용자<br /><br /> 2 = 자동 관리 캐싱<br /><br /> 3 = 지연 처리|  
|ProgressTotal|9|1|보고된 이벤트의 총 진행률을 포함합니다.|  
|IntegerData|10|1|처리 중인 이벤트에 대해 현재 처리된 행 개수와 같이 보고된 이벤트와 연결된 정수 데이터를 포함합니다.|  
|ObjectID|11|8|보고된 이벤트와 연결된 개체 ID(문자열)를 포함합니다.|  
|ObjectType|12|1|개체 유형을 포함합니다.|  
|ObjectName|13|8|보고된 이벤트와 연결된 개체의 이름을 포함합니다.|  
|ObjectPath|14|8|보고된 이벤트와 연결된 개체의 개체 경로를 해당 개체의 부모로 시작하는 부모 목록(쉼표로 구분)으로 포함합니다.|  
|ObjectReference|15|8|모든 부모에 대해 XML로 인코딩되고 개체를 설명하는 태그를 사용하는 보고된 이벤트에 대한 개체 참조를 포함합니다.|  
|Severity|22|1|보고된 이벤트와 연결된 예외의 심각도 수준을 포함합니다. 값은 다음과 같습니다.<br /><br /> 0 = 성공<br /><br /> 1 = 알림<br /><br /> 2 = 경고<br /><br /> 3 = 오류|  
|Error|24|1|지정된 이벤트의 오류 번호를 포함합니다.|  
|ConnectionID|25|1|보고된 이벤트와 연결된 고유 연결 ID를 포함합니다.|  
|DatabaseName|28|8|보고된 이벤트가 발생한 데이터베이스의 이름을 포함합니다.|  
|SessionID|39|8|보고된 이벤트와 연결된 세션 ID를 포함합니다.|  
|SPID|41|1|보고된 이벤트와 연결된 사용자 세션을 고유하게 식별하는 SPID(서버 프로세스 ID)를 포함합니다. SPID는 XMLA(XML for Analysis)에서 사용하는 세션 GUID와 정확히 일치합니다.|  
|TextData|42|9|보고된 이벤트와 연결된 텍스트 데이터를 포함합니다.|  
|데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면|43|8|보고된 이벤트가 발생한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 이름을 포함합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Progress Reports 이벤트 범주](progress-reports-event-category.md)  
  
  