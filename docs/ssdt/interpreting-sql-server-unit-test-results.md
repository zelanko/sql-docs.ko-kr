---
title: SQL Server 단위 테스트 결과 해석 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fde3c95b-2f68-483d-a197-0f7161b72fa3
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1ea9047286b25eaae4820d5b7726a657fa19a22a
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094851"
---
# <a name="interpreting-sql-server-unit-test-results"></a>SQL Server 단위 테스트 결과 해석
SQL Server 단위 테스트를 실행하면 테스트 결과가 자동으로 생성되어 디스크에 저장되고 **테스트 결과** 창에 요약됩니다. 테스트 실행을 시작하는 즉시 **테스트 결과** 창이 나타나고 테스트 실행 진행률이 표시됩니다. 여기에는 실행 중인 테스트 및 완료된 테스트가 포함됩니다.  
  
테스트 결과에 대한 자세한 내용을 보려면 **테스트 결과** 창에서 테스트 결과를 두 번 클릭하여 **테스트 결과 정보** 페이지를 표시합니다. 테스트 결과에 대한 자세한 내용을 보려면 테스트 결과를 두 번 클릭합니다.  
  
**테스트 결과** 창의 표시를 변경하는 방법에 대한 자세한 내용은 [방법: 테스트 창의 열 추가 또는 제거(Visual Studio 2010)](http://msdn.microsoft.com/library/ms182508(VS.100).aspx) 또는 [방법: 테스트 창의 열 추가 또는 제거(Visual Studio 2012)](http://msdn.microsoft.com/library/ms182508.aspx)를 참조하세요.  
  
## <a name="storing-test-results"></a>테스트 결과 저장  
단위 테스트의 결과는 하드 디스크에 확장명이 .trx인 파일로 자동 저장됩니다. .trx 파일은 테스트 실행의 세부 정보가 포함된 XML 파일입니다. 이전 테스트 실행에서 .trx 파일을 로드하여 해당 테스트 실행 결과를 검토하거나 이전 테스트를 다시 실행할 수 있습니다 자세한 내용은 [방법: 테스트 다시 실행(Visual Studio 2010)](http://msdn.microsoft.com/library/ms182472(VS.100).aspx)을 참조하세요.  
  
> [!NOTE]  
> 단위 테스트를 원격으로 실행할 수는 없습니다.  
  
팀에서 Visual Studio Team Foundation Server 팀 프로젝트를 사용하여 작업을 관리하는 경우 테스트 데이터를 작업 저장소라는 SQL Server 데이터베이스에 게시할 수도 있습니다.  
  
테스트 결과를 저장하고 다시 사용하고 팀과 공유하는 방법에 대한 자세한 내용은 [방법: Visual Studio 2010에서 테스트 결과 저장 및 열기](http://msdn.microsoft.com/library/ms404662(VS.100).aspx) 또는 [방법: Visual Studio 2012에서 테스트 결과 저장 및 열기](http://msdn.microsoft.com/library/ms404662.aspx)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 단위 테스트 실행](../ssdt/running-sql-server-unit-tests.md)  
  
