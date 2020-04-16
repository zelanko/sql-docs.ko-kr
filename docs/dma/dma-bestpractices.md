---
title: Data Migration Assistant 모범 사례
description: 데이터 마이그레이션 도우미를 사용하여 SQL Server 데이터베이스를 마이그레이션하는 모범 사례 알아보기
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
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: f2bfbb79a8a4803bb56e3dce85f575e8cf257b4a
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388159"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>Data Migration Assistant 실행 모범 사례
이 문서에서는 설치, 평가 및 마이그레이션에 대한 몇 가지 모범 사례 정보를 제공합니다.

## <a name="installation"></a>설치
SQL Server 호스트 컴퓨터에서 직접 데이터 마이그레이션 도우미를 설치하고 실행하지 마십시오.

## <a name="assessment"></a>평가
- 사용량이 비아닌 시간에 프로덕션 데이터베이스에 대한 평가를 실행합니다.
- 호환성 **문제** 및 **새로운 기능 권장 사항** 평가를 별도로 수행하여 평가 기간을 줄입니다.

## <a name="migration"></a>마이그레이션
- 사용량이 비많은 시간에 서버를 마이그레이션합니다.

- 데이터베이스를 마이그레이션할 때 원본 서버와 대상 서버에서 액세스할 수 있는 단일 공유 위치를 제공하고 가능한 경우 복사 작업을 피하십시오. 복사 작업은 백업 파일의 크기에 따라 지연이 발생할 수 있습니다. 또한 복사 작업은 추가 단계로 인해 마이그레이션이 실패할 가능성을 높입니다. 단일 위치가 제공되면 데이터 마이그레이션 도우미가 복사 작업을 무시합니다.
 
    또한 마이그레이션 실패를 방지하기 위해 공유 폴더에 올바른 권한을 제공해야 합니다. 올바른 사용 권한이 도구에 지정됩니다. SQL Server 인스턴스가 네트워크 서비스 자격 증명으로 실행되는 경우 SQL Server 인스턴스에 대한 컴퓨터 계정에 공유 폴더에 대한 올바른 권한을 부여합니다.

- 원본 및 대상 서버에 연결할 때 암호화 연결을 사용하도록 설정합니다. TLS 암호화를 사용하면 데이터 마이그레이션 도우미와 SQL Server 인스턴스 간에 네트워크를 통해 전송되는 데이터의 보안이 향상되며, 특히 SQL 로그인을 마이그레이션할 때 유용합니다. TLS 암호화가 사용되지 않고 공격자가 네트워크를 손상시키면 마이그레이션중인 SQL 로그인이 공격자가 가로채거나 즉시 수정될 수 있습니다.

    그러나 모든 액세스가 보안 인트라넷 구성과 관련된 경우 암호화가 필요하지 않을 수도 있습니다. 암호화를 사용하도록 설정하면 패킷을 암호화하고 해독하는 데 필요한 추가 오버헤드가 때문에 성능이 저하됩니다. 자세한 내용은 [SQL Server에 대한 연결 암호화를](https://go.microsoft.com/fwlink/?linkid=832513)참조하십시오.
    
- 데이터를 마이그레이션하기 전에 원본 데이터베이스와 대상 데이터베이스 모두에서 신뢰할 수 없는 제약 조건이 있는지 확인합니다. 마이그레이션 후 대상 데이터베이스를 다시 분석하여 데이터 이동의 일부로 제약 조건이 신뢰할 수 없는지 확인합니다. 필요에 따라 신뢰할 수 없는 제약 조건을 수정합니다. 제약 조건을 신뢰할 수 없는 상태로 두면 실행 계획이 저하될 수 있으며 성능에 영향을 줄 수 있습니다.
