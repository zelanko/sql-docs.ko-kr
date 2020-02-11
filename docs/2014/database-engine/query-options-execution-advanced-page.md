---
title: 쿼리 옵션 실행 (고급 페이지) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.advanced.f1
ms.assetid: 661595ce-99b9-4316-ad80-ed04002d04d5
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: ''
ms.custom: ''
ms.date: 09/03/2019
ms.openlocfilehash: 39a43adeb82b154a076fc7bfc24cc56b54cc8640
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "71199330"
---
# <a name="query-options-execution-advanced-page"></a>쿼리 옵션 실행(고급 페이지)

  
  **SET** 문을 사용하여 다양한 옵션을 사용할 수 있습니다. 이 페이지를 사용 하 여 Microsoft SQL Server 쿼리를 실행 하는 **SET** 옵션을 지정할 수 있습니다. 이러한 각 옵션에 대한 자세한 내용은 SQL Server 온라인 설명서를 참조하십시오.
  
**SET NOCOUNT** 는 결과 집합이 포함 된 메시지로 행의 수를 반환 하지 않습니다. 이 옵션은 기본적으로 선택 취소되어 있습니다.

**NOEXEC 설정** 쿼리를 실행 하지 않습니다. 이 옵션은 기본적으로 선택 취소되어 있습니다.

**PARSEONLY 설정** 각 쿼리의 구문을 검사 하지만 쿼리를 실행 하지는 않습니다. 이 옵션은 기본적으로 선택 취소되어 있습니다.  

**CONCAT_NULL_YIELDS_NULL 설정** 이 확인란을 선택 하면 기존 값을와 `NULL`연결 하는 쿼리는 항상를 `NULL` 결과로 반환 합니다. 이 확인란의 선택을 취소하면 `NULL`에 연결된 기존 값이 기존 값을 반환합니다. 이 옵션은 기본적으로 선택되어 있습니다.

**ARITHABORT 설정** 이 확인란을 선택 하면 식을 평가 하는 `INSERT`동안 `DELETE` , `UPDATE` 또는 문에 산술 오류 (오버플로, 0으로 나누기 또는 도메인 오류)가 발생할 때 쿼리 또는 일괄 처리가 종료 됩니다. 이 확인란의 선택을 취소하면 가능한 경우 해당 값으로 `NULL` 이 제공되고 쿼리가 계속된 다음 결과에 메시지가 포함됩니다. 이 동작에 대한 자세한 설명은 온라인 설명서를 참조하십시오. 이 옵션은 기본적으로 선택되어 있습니다.
  
**SHOWPLAN_TEXT 설정** 이 확인란을 선택 하면 각 쿼리를 사용 하 여 쿼리 계획이 텍스트 형식으로 반환 됩니다. 이 옵션은 기본적으로 선택 취소되어 있습니다.
  
**통계 시간 설정** 이 확인란을 선택 하면 각 쿼리와 함께 시간 통계가 반환 됩니다. 이 옵션은 기본적으로 선택 취소되어 있습니다.
  
**통계 IO 설정** 이 확인란을 선택 하면 각 쿼리와 함께 i/o (입/출력) 관련 통계가 반환 됩니다. 이 옵션은 기본적으로 선택 취소되어 있습니다.
  
**트랜잭션 격리 수준 설정** 커밋된 읽기 트랜잭션 격리 수준은 기본적으로 설정 되어 있습니다. 자세한 내용은 [SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)을 참조하세요. SNAPSHOT 트랜잭션 격리 수준을 사용할 수 없습니다. SNAPSHOT 격리를 사용하려면 다음 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 추가합니다.
  
  ```sql
  SET TRANSACTION ISOLATION LEVEL SNAPSHOT;
  GO
  ```

**교착 상태 우선 순위 설정** 기본값 **Normal** 은 교착 상태가 발생할 때 각 쿼리가 동일한 우선 순위를 가질 수 있도록 합니다. 이 쿼리를 교착 상태를 해제하고 종료할 쿼리로 선택하려면 드롭다운 목록에서 Low 우선 순위를 선택합니다.

**잠금 제한 시간 설정** 기본값-1은 트랜잭션이 완료 될 때까지 잠금이 유지 됨을 나타냅니다. 0은 기다리지 않음을 나타내고 잠금이 있으면 바로 오류 메시지가 반환됩니다. 트랜잭션 잠금을 이 시간보다 오래 유지해야 하는 경우 0밀리초보다 큰 값을 지정하여 트랜잭션을 종료합니다.

**QUERY_GOVERNOR_COST_LIMIT 설정** Query **governor cost limit** 옵션을 사용 하 여 쿼리가 실행 될 수 있는 기간의 상한을 지정할 수 있습니다. 쿼리 비용이란 특정 하드웨어 구성에서 쿼리를 완료하는 데 필요한 예상 소요 시간(초)입니다. 기본값 0은 쿼리 실행 제한 시간이 없다는 것을 나타냅니다.

**공급자 메시지 헤더 표시 안 함** 이 확인란을 선택 하면 공급자의 상태 메시지 (예: OLE DB 공급자)가 표시 되지 않습니다. 이 확인란은 기본적으로 선택되어 있습니다. 공급자 수준에서 오류가 발생할 수 있는 쿼리 문제를 해결할 때 공급자 메시지를 보려면 이 확인란의 선택을 취소합니다.

**쿼리가 실행 된 후 연결 끊기** 이 확인란을 선택 하면 쿼리가 완료 된 후 SQL Server에 대 한 연결이 종료 됩니다. 이 옵션은 기본적으로 선택 취소되어 있습니다.

**완료 시간 표시** 쿼리 결과 또는 메시지 탭 후에 쿼리 실행이 완료 된 시간을 인쇄할 수 있습니다.

**Always Encrypted에 대 한 VBS enclaves 용 증명 프로토콜** Secure enclaves로 상시 암호화에 사용 되는 VBS (가상화 기반 보안) enclaves 증명 프로토콜을 설정할 수 있습니다.

현재 지원 되는 증명 프로토콜은 다음과 같습니다.

* 호스트 보호 서비스-Windows HGS (호스트 보호 서비스)를 사용 하는 증명 프로토콜입니다.

자세한 내용은 [secure enclaves](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves?view=sqlallproducts-allversions) 및 [secure Enclave 증명](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves?view=sqlallproducts-allversions#secure-enclave-attestation)을 사용 하는 Always Encrypted를 참조 하세요.

**기본값으로 다시 설정** 이 페이지의 모든 값을 원래 기본값으로 다시 설정 합니다.
