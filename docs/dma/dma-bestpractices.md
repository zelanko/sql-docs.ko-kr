---
title: Data Migration Assistant (SQL Server)에 대 한 모범 사례 | Microsoft Docs
description: Data Migration Assistant를 사용 하 여 SQL Server 데이터베이스 마이그레이션에 대 한 모범 사례를 알아봅니다.
ms.custom: ''
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Best Practices
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: 5a717c47163e03e6430272ca44d2120c7328289e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061779"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>Data Migration Assistant를 실행 하기 위한 모범 사례
이 문서에서는 설치, 평가 및 마이그레이션에 대 한 몇 가지 모범 사례 정보를 제공 합니다.

## <a name="installation"></a>설치
설치 하 고 Data Migration Assistant는 SQL Server 호스트 컴퓨터에서 직접 실행 하지 마십시오.

## <a name="assessment"></a>평가
- 사용량이 많지 않은 시간 동안 프로덕션 데이터베이스에서 평가 실행 합니다.
- 수행 합니다 **호환성 문제** 하 고 **새로운 기능 권장** 평가 기간을 축소를 개별적으로 평가 합니다.

## <a name="migration"></a>마이그레이션
- 사용량이 많지 않은 시간 동안 서버를 마이그레이션하십시오.

- 데이터베이스를 마이그레이션하는 경우 원본 서버 및 대상 서버에 액세스할 수 있는 단일 공유 위치를 제공 하 고 복사 작업을 가능한 경우 방지 합니다. 복사 작업을 백업 파일의 크기를 기준으로 하는 지연이 발생할 수 있습니다. 복사 작업에는 또한 마이그레이션을 추가 단계를 실패 가능성이 증가 합니다. Data Migration Assistant에서는 단일 위치를 제공 하는 경우 복사 작업을 건너뜁니다.
 
    또한 해야 마이그레이션 오류를 방지 하려면 공유 폴더에 올바른 사용 권한을 제공 하는 합니다. 도구에서 올바른 사용 권한이 지정 됩니다. 네트워크 서비스 자격 증명으로 SQL Server 인스턴스를 실행 하는 경우 SQL Server 인스턴스에 대 한 컴퓨터 계정에 공유 폴더에 올바른 권한을 부여 합니다.

- 원본 및 대상 서버에 연결할 때 연결을 암호화 하는 사용 하도록 설정 합니다. SSL을 사용 하 여 암호화 Data Migration Assistant 및 SQL 로그인을 마이그레이션하는 경우에 특히 도움이 되는 SQL Server 인스턴스 간에 네트워크를 통해 전송 되는 데이터의 보안을 강화 합니다. SSL 암호화 사용 되지 않는 경우 공격자가 네트워크를 손상 시킬 마이그레이션되는 SQL 로그인 차단할 수 있습니다 하거나에 즉석 공격자가 수정 합니다.

    그러나 모든 액세스가 보안 인트라넷 구성과 관련된 경우 암호화가 필요하지 않을 수도 있습니다. 암호화를 사용 하도록 설정 하면 이기 암호화 및 패킷 암호 해독 하는 데 필요한 추가적인 오버 헤드 때문에 성능이 느려집니다. 자세한 내용은 참조 하십시오 [SQL Server 연결 암호화](https://go.microsoft.com/fwlink/?linkid=832513)합니다.
