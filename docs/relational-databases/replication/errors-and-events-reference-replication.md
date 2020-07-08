---
title: 오류 및 이벤트 참조(복제) | Microsoft 문서
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server replication], troubleshooting
- troubleshooting [SQL Server replication], errors
- replication [SQL Server], troubleshooting
- errors [SQL Server replication]
- errors and events reference [SQL Server replication]
ms.assetid: e67d1bab-47b6-441d-ab9c-251a2ca499e1
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 273caba1a25efbfd30bb856f6ebaf157b9bf5a03
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85652990"
---
# <a name="errors-and-events-reference-replication"></a>오류 및 이벤트 참조(복제)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  설명서의 이 섹션에는 복제와 관련된 다양한 오류의 원인 및 해결 방법에 대한 정보가 포함되어 있습니다.  
  
|Error|메시지|  
|-----------|-------------|  
|[MSSQL_ENG002601](../../relational-databases/replication/mssql-eng002601.md)|고유 인덱스가 '%.\*ls'인 개체 '%.*ls'에 중복 키 행을 삽입할 수 없습니다.|  
|[MSSQL_ENG002627](../../relational-databases/replication/mssql-eng002627.md)|%ls 제약 조건 '%.*ls'을(를) 위반했습니다. 개체 '%.\*ls'에 중복 키를 삽입할 수 없습니다.|  
|[MSSQL_ENG003165](../../relational-databases/replication/mssql-eng003165.md)|데이터베이스 '%ls'이(가) 복원되었지만 복제가 복원/제거되는 동안 오류가 발생했습니다. 데이터베이스가 오프라인 상태로 남아 있습니다. SQL Server 온라인 설명서의 MSSQL_ENG003165 항목을 참조하십시오.|  
|[MSSQL_ENG003724](../../relational-databases/replication/mssql-eng003724.md)|%S_MSG '%.*ls'은(는) 복제에 사용 중이므로 %S_MSG할 수 없습니다.|  
|[MSSQL_ENG004929](../../relational-databases/replication/mssql-eng004929.md)|%S_MSG '%.*ls'은(는) 복제용으로 게시 중이므로 변경할 수 없습니다.|  
|MSSQL_ENG007395. [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)을 참조하세요.|연결된 서버 "%ls"의 OLE DB 공급자 "%ls"에 대해 중첩 트랜잭션을 시작할 수 없습니다. XACT_ABORT 옵션이 OFF로 설정되어 있으므로 중첩 트랜잭션이 필요합니다.|  
|[MSSQL_ENG014005](../../relational-databases/replication/mssql-eng014005.md)|게시를 삭제할 수 없습니다. 게시에 대한 구독이 존재합니다.|  
|[MSSQL_ENG014010](../../relational-databases/replication/mssql-eng014010.md)|서버 '%s'이(가) 구독 서버로 정의되지 않았습니다.|  
|[MSSQL_ENG014114](../../relational-databases/replication/mssql-eng014114.md)|'%s'이(가) 배포자로 구성되지 않았습니다.|  
|[MSSQL_ENG014117](../../relational-databases/replication/mssql-eng014117.md)|'%s'이(가) 배포 데이터베이스로 구성되지 않았습니다.|  
|[MSSQL_ENG014120](../../relational-databases/replication/mssql-eng014120.md)|배포 데이터베이스 '%s'을(를) 삭제할 수 없습니다. 이 배포자 데이터베이스가 게시자와 연관되어 있습니다.|  
|[MSSQL_ENG014121](../../relational-databases/replication/mssql-eng014121.md)|배포자 '%s'을(를) 삭제할 수 없습니다. 이 배포자가 배포 데이터베이스와 연관되어 있습니다.|  
|[MSSQL_ENG014144](../../relational-databases/replication/mssql-eng014144.md)|구독자 '%s'을(를) 삭제할 수 없습니다. 게시 데이터베이스 '%s'에 이 구독자에 대한 구독이 있습니다.|  
|[MSSQL_ENG014150](../../relational-databases/replication/mssql-eng014150.md)|복제-%s: 에이전트 %s이(가) 성공했습니다. %s|  
|[MSSQL_ENG014151](../../relational-databases/replication/mssql-eng014151.md)|복제-%s: 에이전트 %s이(가) 실패했습니다. %s|  
|[MSSQL_ENG014152](../../relational-databases/replication/mssql-eng014152.md)|복제-%s: 에이전트 %s이(가) 다시 시도하도록 예약되었습니다. %s|  
|[MSSQL_ENG014157](../../relational-databases/replication/mssql-eng014157.md)|구독자 '%s'이(가) 게시 '%s'에 대해 만든 구독이 만료되어 삭제되었습니다.|  
|[MSSQL_ENG014160](../../relational-databases/replication/mssql-eng014160.md)|게시 [%s]에 대한 임계값 [%s:%s]이(가) 설정되어 있습니다. 병합 에이전트가 실행 중이고 필요한 요구 사항에 맞는지 확인하십시오. 이 게시에 대해 하나 이상의 구독이 만료되었습니다.|  
|[MSSQL_ENG014161](../../relational-databases/replication/mssql-eng014161.md)|게시 [%s]에 대한 임계값 [%s:%s]이(가) 설정되어 있습니다. 병합 에이전트가 실행 중이고 필요한 요구 사항에 맞는지 확인하십시오. 로그 판독기와 배포 에이전트가 실행 중이고 대기 시간 요구 사항에 맞는지 확인하십시오.|  
|[MSSQL_ENG014162](../../relational-databases/replication/mssql-eng014162.md)|게시 [%s]에 대한 임계값 [%s:%s]이(가) 설정되어 있습니다. 병합 에이전트가 실행 중이고 필요한 요구 사항에 맞는지 확인하십시오. 병합 에이전트가 실행 중이고 필요한 요구 사항에 맞는지 확인하십시오.|  
|[MSSQL_ENG014163](../../relational-databases/replication/mssql-eng014163.md)|게시 [%s]에 대한 임계값 [%s:%s]이(가) 설정되어 있습니다. 병합 에이전트가 실행 중이고 필요한 요구 사항에 맞는지 확인하십시오. 병합 에이전트가 실행 중이고 필요한 요구 사항에 맞는지 확인하십시오.|  
|[MSSQL_ENG014164](../../relational-databases/replication/mssql-eng014164.md)|게시 [%s]에 대한 임계값 [%s:%s]이(가) 설정되어 있습니다. 병합 에이전트가 실행 중이고 필요한 요구 사항에 맞는지 확인하십시오. 병합 에이전트가 실행 중이고 필요한 요구 사항에 맞는지 확인하십시오.|  
|[MSSQL_ENG014165](../../relational-databases/replication/mssql-eng014165.md)|게시 [%s]에 대한 임계값 [%s:%s]이(가) 설정되어 있습니다. 병합 에이전트가 실행 중이고 필요한 요구 사항에 맞는지 확인하십시오. 병합 에이전트가 실행 중이고 필요한 요구 사항에 맞는지 확인하십시오.|  
|[MSSQL_ENG018456](../../relational-databases/replication/mssql-eng018456.md)|사용자 '%.*ls'이(가) 로그인하지 못했습니다.%.\*ls|  
|[MSSQL_ENG018752](../../relational-databases/replication/mssql-eng018752.md)|한 번에 하나의 로그 판독기 에이전트 또는 로그 관련 프로시저(sp_repldone, sp_replcmds 및 sp_replshowcmds)만 데이터베이스에 연결할 수 있습니다. 로그 관련 프로시저를 실행한 경우 로그 판독기 에이전트를 시작하거나 다른 로그 관련 프로시저를 실행하기 전에 프로시저가 실행된 연결을 삭제하거나 해당 연결에 대해 sp_replflush를 실행하십시오.|  
|[MSSQL_ENG020554](../../relational-databases/replication/mssql-eng020554.md)|복제 에이전트가 %ld분 동안 진행률 메시지를 로깅하지 않았습니다. 이것은 에이전트가 응답하지 않거나 시스템 작업이 많음을 나타낼 수 있습니다. 레코드가 대상으로 복제되고 구독자, 게시자 및 배포자에 대한 연결이 여전히 활성 상태인지 확인하십시오.|  
|[MSSQL_ENG020557](../../relational-databases/replication/mssql-eng020557.md)|에이전트를 종료합니다. 자세한 내용은 작업 '%s'에 대한 SQL Server 에이전트 작업 기록을 참조하십시오.|  
|[MSSQL_ENG020572](../../relational-databases/replication/mssql-eng020572.md)|게시 '%s'의 아티클 '%s'에 대한 구독자 '%s'의 구독이 유효성 검사 실패 후 다시 초기화되었습니다.|  
|[MSSQL_ENG020574](../../relational-databases/replication/mssql-eng020574.md)|게시 '%s'의 아티클 '%s'에 대한 구독자 '%s'의 구독이 데이터 유효성 검사에 실패했습니다.|  
|[MSSQL_ENG020575](../../relational-databases/replication/mssql-eng020575.md)|게시 '%s'의 아티클 '%s'에 대한 구독자 '%s'의 구독이 데이터 유효성 검사를 통과했습니다.|  
|[MSSQL_ENG020596](../../relational-databases/replication/mssql-eng020596.md)|'%s' 또는 db_owner의 멤버만 익명 에이전트를 삭제할 수 있습니다.|  
|[MSSQL_ENG020598](../../relational-databases/replication/mssql-eng020598.md)|복제된 명령을 적용하는 동안 구독자에서 행을 찾을 수 없습니다.|  
|[MSSQL_ENG021075](../../relational-databases/replication/mssql-eng021075.md)|게시 '%s'의 초기 스냅샷을 사용할 수 없습니다.|  
|[MSSQL_ENG021076](../../relational-databases/replication/mssql-eng021076.md)|아티클 '%s'의 초기 스냅샷을 아직 사용할 수 없습니다.|  
|[MSSQL_ENG021286](../../relational-databases/replication/mssql-eng021286.md)|충돌 테이블 '%s'이(가) 없습니다.|  
|[MSSQL_ENG021330](../../relational-databases/replication/mssql-eng021330.md)|복제 작업 디렉터리(%ls)에 하위 디렉터리를 만들지 못했습니다.|  
|[MSSQL_ENG021331](../../relational-databases/replication/mssql-eng021331.md)|사용자 스크립트 파일을 배포자(%ls)에 복사하지 못했습니다.|  
|[MSSQL_ENG021385](../../relational-databases/replication/mssql-eng021385.md)|스냅샷이 게시 '%s'을(를) 처리하지 못했습니다. 활성 스키마 변경 작업 또는 추가 중인 새 아티클 때문인 것 같습니다.|  
|MSSQL_ENG021617. [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)을 참조하세요.|SQL*PLUS를 실행할 수 없습니다. 배포자에 최신 버전의 Oracle 클라이언트 코드가 설치되었는지 확인하십시오.|  
|MSSQL_ENG021620. [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)을 참조하세요.|시스템 경로 변수로 액세스할 수 있는 SQL*PLUS 버전이 최신 버전이 아니어서 Oracle 게시를 지원할 수 없습니다. 배포자에 최신 버전의 Oracle 클라이언트 코드가 설치되었는지 확인하십시오.|  
|MSSQL_ENG021624. [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)을 참조하세요.|배포자 '%s'에서 Oracle OLEDB 공급자 OraOLEDB.Oracle을 찾을 수 없습니다. 배포자에 최신 버전의 Oracle OLEDB 공급자가 설치 및 등록되었는지 확인하십시오.|  
|MSSQL_ENG021626. [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)을 참조하세요.|Oracle OLEDB 공급자 OraOLEDB.Oracle을 사용하여 Oracle 데이터베이스 서버 '%s'에 연결할 수 없습니다.|  
|MSSQL_ENG021627. [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)을 참조하세요.|Microsoft OLEDB 공급자 MSDAORA를 사용하여 Oracle 데이터베이스 서버 '%s'에 연결할 수 없습니다.|  
|MSSQL_ENG021628. [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)을 참조하세요.|Oracle OLEDB 공급자 OraOLEDB.Oracle이 SQL Server 프로세스에서 실행되도록 허용하기 위해 배포자 '%s'의 레지스트리를 업데이트할 수 없습니다. 현재 로그인에 SQL Server 소유 레지스트리 키를 수정할 권한이 부여되었는지 확인하십시오.|  
|MSSQL_ENG021629. [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)을 참조하세요.|Oracle OLEDB 공급자 OraOLEDB.Oracle이 등록되었음을 나타내는 CLSID 레지스트리 키가 배포자에 없습니다. 배포자에 Oracle OLEDB 공급자가 설치 및 등록되었는지 확인하십시오.|  
|MSSQL_ENG021642. [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)을 참조하세요.|유형이 다른 게시자에는 연결된 서버가 필요합니다. 이름이 '%s'인 연결된 서버가 이미 있습니다. 연결된 서버를 제거하거나 다른 게시자 이름을 선택하십시오.|  
|MSSQL_ENG021663. [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)을 참조하세요.|원본 테이블 [%s].[%s]에 대해 올바른 기본 키를 찾을 수 없습니다.|  
|MSSQL_ENG021684. [Troubleshooting Oracle Publishers](../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)을 참조하세요.|Oracle 게시자 '%s'의 관리자 로그인과 연관된 사용 권한이 충분하지 않습니다.|  
|[MSSQL_ENG021797](../../relational-databases/replication/mssql-eng021797.md)|'%s'은(는) '컴퓨터\\로그인' 또는 '도메인\\로그인' 형식의 올바른 Windows 로그인이어야 합니다. '%s'에 대한 설명서를 참조하십시오.|  
|[MSSQL_ENG021798](../../relational-databases/replication/mssql-eng021798.md)|계속하려면 먼저 '%s'을(를) 통해 '%s' 에이전트 작업을 추가해야 합니다. '%s'에 대한 설명서를 참조하십시오.|  
|[MSSQL_REPL020011](../../relational-databases/replication/mssql-repl020011.md)|'%2'에서 '%1'을(를) 실행할 수 없습니다.|  
|[MSSQL_REPL027056](../../relational-databases/replication/mssql-repl027056.md)|병합 프로세스에서 '%1'의 생성 기록을 변경할 수 없습니다. 문제를 해결하려면 자세한 기록 로깅으로 동기화를 다시 시작하고 기록할 출력 파일을 지정하십시오.|  
|[MSSQL_REPL027183](../../relational-databases/replication/mssql-repl027183.md)|병합 프로세스에서 매개 변수가 있는 행 필터를 사용하여 아티클의 변경 내용을 열거하지 못했습니다. 이 오류가 계속되면 이 프로세스에 대한 쿼리 제한 시간을 늘리고 게시 보존 기간을 줄인 다음 게시된 테이블의 인덱스를 향상시키십시오.|  
  
  
