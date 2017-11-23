---
title: "데이터 마이그레이션 길잡이 (SQL Server)에 대 한 모범 사례 | Microsoft Docs"
ms.custom: 
ms.date: 10/04/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: 
ms.component: dma
ms.reviewer: 
ms.suite: sql
ms.technology: sql-dma
ms.tgt_pltfrm: 
ms.topic: article
keywords: 
helpviewer_keywords: Data Migration Assistant, Best Practices
ms.assetid: 
caps.latest.revision: 
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e362128482bab8f2447aceb8294cf5ea41167210
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="best-practices-for-running-data-migration-assistant"></a>데이터 마이그레이션 길잡이 실행 하기 위한 모범 사례
이 문서에서는 설치, 평가 및 마이그레이션에 대 한 다음과 같은 모범 사례 정보를 제공 합니다.

## <a name="installation"></a>설치

설치 하 고 SQL Server 호스트 컴퓨터에서 직접 데이터 마이그레이션 길잡이 실행 하지 마십시오.

## <a name="assessment"></a>평가

- 사용량이 많지 않은 시간 동안 프로덕션 데이터베이스에서 평가 실행 합니다.

- 수행 된 **호환성 문제** 및 **새 기능 권장** 평가 기간 축소를 개별적으로 평가 합니다.

## <a name="migration"></a>마이그레이션

- 사용량이 많지 않은 시간 동안 서버를 마이그레이션하십시오.

- 데이터베이스를 마이그레이션하는 경우 원본 서버와 대상 서버에서 액세스할 수 있는 단일 공유 위치를 지정 하 고 가능한 경우 복사 작업을 방지 합니다. 복사 작업을 백업 파일의 크기에 따라 지연이 발생할 수 있습니다. 복사 작업에는 또한 별도 단계 때문에 실패 한 마이그레이션 상태의 발생 가능성이 증가 합니다. 단일 위치를 제공 하는 경우 복사 작업이 데이터 Migration Assistant 무시 합니다.
 
    또한 해야 마이그레이션 오류를 방지 하려면 공유 폴더에 올바른 사용 권한을 제공 하 합니다. 이 도구에 올바른 사용 권한이 지정 됩니다. SQL Server 인스턴스가 네트워크 서비스 자격 증명으로 실행 되는 경우 SQL Server 인스턴스에 대 한 컴퓨터 계정에 공유 폴더에 올바른 사용 권한을 부여 합니다.

- 원본 및 대상 서버에 연결할 때 연결을 암호화 하는 사용 하도록 설정 합니다. SSL을 사용 하 여 암호화 데이터 Migration Assistant 및 SQL Server 인스턴스 간의 네트워크를 통해 전송 되는 데이터의 보안을 향상 시킵니다. 이 SQL 로그인을 마이그레이션하는 경우에 특히 유용 합니다. SSL 암호화는 사용 되지 않으며 공격자가 네트워크를 손상 시킬, 하는 경우 마이그레이션 중인 SQL 로그인 차단할 수 및/또는에 즉시는 공격자에 의해 수정 합니다.

    그러나 모든 액세스가 보안 인트라넷 구성과 관련된 경우 암호화가 필요하지 않을 수도 있습니다. 암호화를 사용 하도록 설정 하면 암호화 및 패킷이 암호 해독 하는 데 필요한 오버 헤드 추가 결과로 성능이 느려집니다. 자세한 내용은를 참조 하십시오 [SQL Server 연결 암호화](https://go.microsoft.com/fwlink/?linkid=832513)합니다.
