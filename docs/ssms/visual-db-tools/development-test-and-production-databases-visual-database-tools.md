---
title: 개발, 테스트 및 프로덕션 데이터베이스 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- production databases [SQL Server]
- testing databases
- database testing [SQL Server]
ms.assetid: cb403330-8cbe-41c6-bd23-bc432d50f173
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f667fd107935eb0373e7d3ee0c1fcaa2711b8776
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68254805"
---
# <a name="development-test-and-production-databases-visual-database-tools"></a>개발, 테스트 및 프로덕션 데이터베이스(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
동일한 구조의 데이터베이스가 두 개 있으면 한 데이터베이스에서 변경한 내용을 다른 데이터베이스로 전파할 수 있습니다. 예를 들어, 개인 개발 데이터베이스와 그룹 범위의 테스트 데이터베이스가 있는 경우 개발 데이터베이스를 수정한 다음 해당 수정 내용을 테스트 데이터베이스로 전파할 수 있습니다.  
  
이를 위해서는 개발 데이터베이스를 사용하여 단일 세션에서 모든 수정 작업을 수행하고 해당 세션에 대한 변경 스크립트를 만든 다음 테스트 데이터베이스에 대해 이 스크립트를 실행해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
[다중 사용자 환경&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/multiuser-environments-visual-database-tools.md)  
  
