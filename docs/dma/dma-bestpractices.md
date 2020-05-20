---
title: Data Migration Assistant 모범 사례
description: Data Migration Assistant를 사용 하 여 SQL Server 데이터베이스 마이그레이션에 대 한 모범 사례를 알아봅니다.
ms.custom: seo-lt-2019
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
author: rajeshsetlem
ms.author: rajpo
ms.openlocfilehash: fbfc995b3271c9618cd773d42d3e8154958d6af5
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82886050"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>Data Migration Assistant 실행 모범 사례
이 문서에서는 설치, 평가 및 마이그레이션에 대 한 몇 가지 모범 사례 정보를 제공 합니다.

## <a name="installation"></a>설치
SQL Server 호스트 컴퓨터에서 직접 Data Migration Assistant를 설치 하 고 실행 하지 마세요.

## <a name="assessment"></a>평가
- 사용량이 많지 않은 시간 동안 프로덕션 데이터베이스에서 평가를 실행 합니다.
- **호환성 문제** 및 **새 기능 권장 사항** 평가를 별도로 수행 하 여 평가 기간을 줄이십시오.

## <a name="migration"></a>마이그레이션
- 사용량이 많지 않은 시간에 서버를 마이그레이션합니다.

- 데이터베이스를 마이그레이션할 때 원본 서버와 대상 서버에서 액세스할 수 있는 단일 공유 위치를 제공 하 고 가능 하면 복사 작업을 방지 합니다. 복사 작업을 수행 하면 백업 파일의 크기에 따라 지연이 발생할 수 있습니다. 또한 복사 작업을 수행 하면 추가 단계로 인해 마이그레이션이 실패할 가능성이 높아집니다. 단일 위치를 제공 하면 Data Migration Assistant 복사 작업을 무시 합니다.
 
    또한 마이그레이션 실패를 방지 하기 위해 공유 폴더에 대 한 올바른 권한을 제공 해야 합니다. 도구에 올바른 권한이 지정 되어 있습니다. SQL Server 인스턴스가 네트워크 서비스 자격 증명으로 실행 되는 경우 공유 폴더에 대 한 올바른 권한을 SQL Server 인스턴스의 컴퓨터 계정에 부여 합니다.

- 원본 및 대상 서버에 연결할 때 연결 암호화를 사용 하도록 설정 합니다. TLS 암호화를 사용 하면 Data Migration Assistant와 SQL Server 인스턴스 간에 네트워크를 통해 전송 되는 데이터의 보안이 강화 되므로 특히 SQL 로그인을 마이그레이션할 때 유용 합니다. TLS 암호화를 사용 하지 않고 공격자가 네트워크를 손상 시킨 경우 마이그레이션되는 SQL 로그인이 공격자에 의해 즉시 가로채기 및/또는 수정 될 수 있습니다.

    그러나 모든 액세스가 보안 인트라넷 구성과 관련된 경우 암호화가 필요하지 않을 수도 있습니다. 암호화를 사용 하면 패킷을 암호화 하 고 해독 하는 데 필요한 추가 오버 헤드가 발생 하기 때문에 성능이 저하 됩니다. 자세한 내용은 [SQL Server에 대 한 연결 암호화](https://go.microsoft.com/fwlink/?linkid=832513)를 참조 하세요.
    
- 데이터를 마이그레이션하기 전에 원본 데이터베이스와 대상 데이터베이스에 대 한 신뢰할 수 없는 제약 조건을 확인 하십시오. 마이그레이션 후 대상 데이터베이스를 다시 분석 하 여 데이터 이동의 일부로 제약 조건이 신뢰할 수 없게 된 것을 확인 합니다. 필요에 따라 신뢰할 수 없는 제약 조건을 수정 합니다. 제약 조건을 신뢰할 수 없는 상태로 두면 실행 계획이 잘못 될 수 있으며 성능에 영향을 줄 수 있습니다.
