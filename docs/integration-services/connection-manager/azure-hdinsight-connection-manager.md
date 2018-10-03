---
title: Azure HDInsight 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPHDICM.F1
- SQL14.DTS.DESIGNER.AFPHDICM.F1
ms.assetid: 29d01bd9-8b38-43b1-b937-67f8aea57c0f
author: Lingxi-Li
ms.author: lingxl
manager: craigg
ms.openlocfilehash: 1578b71f898f02450b90d9e6f7c20473f6ffed35
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47763291"
---
# <a name="azure-hdinsight-connection-manager"></a>Azure HDInsight 연결 관리자
**Azure HDInsight 연결 관리자**를 통해 SSIS 패키지는 Azure HDInsight 클러스터에 연결할 수 있습니다.

**Azure HDInsight 연결 관리자**는 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.

**Azure HDInsight 연결 관리자**를 만들고 구성하려면 다음 단계를 수행합니다.

1. **SSIS 연결 관리자 추가** 대화 상자에서 **AzureHDInsight**를 선택하고 **추가**를 클릭합니다.
2. **Azure HDInsight 연결 관리자 편집기** 대화 상자에서 연결할 HDInsight 클러스터에 대한 **클러스터 DNS 이름**(프로토콜 접두사 없이), **사용자 이름** 및 **암호**를 지정합니다.
3. **확인** 을 클릭하여 대화 상자를 닫습니다.
4. 작성한 연결 관리자의 속성은 **속성** 창에서 확인할 수 있습니다.
