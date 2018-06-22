---
title: 암호화된 열의 데이터 복제(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- encryption [SQL Server], replicating data
- encryption [SQL Server replication]
- publishing [SQL Server replication], encrypted columns
ms.assetid: d1f8f586-e5a3-4a71-9391-11198d42bfa3
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f3930b53b69e4ee67d624d920da6272d3de0fb8e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081798"
---
# <a name="replicate-data-in-encrypted-columns-sql-server-management-studio"></a>암호화된 열의 데이터 복제(SQL Server Management Studio)
  복제를 사용하여 암호화된 열 데이터를 게시할 수 있습니다. 구독자에서 이 데이터를 해독하고 사용하려면 게시자에서 데이터 암호화에 사용된 키가 구독자에도 있어야 합니다. 복제에서는 암호화 키를 전송하는 보안 메커니즘을 제공하지 않습니다. 구독자에서 직접 암호화 키를 다시 만들어야 합니다. 이 항목에서는 게시자에서 열을 암호화하고 구독자에서 암호화 키를 사용할 수 있게 하는 방법을 보여 줍니다.  
  
 기본 단계는 다음과 같습니다.  
  
1.  게시자에서 대칭 키를 만듭니다.  
  
2.  대칭 키를 사용하여 열 데이터를 암호화합니다.  
  
3.  암호화된 열이 있는 테이블을 게시합니다.  
  
4.  게시를 구독합니다.  
  
5.  구독을 초기화합니다.  
  
6.  ALGORITHM, KEY_SOURCE 및 IDENTITY_VALUE에 대해 1단계와 동일한 값을 사용하여 구독자에서 대칭 키를 다시 만듭니다.  
  
7.  암호화된 열 데이터에 액세스합니다.  
  
> [!NOTE]  
>  대칭 키를 사용하여 열 데이터를 암호화해야 합니다. 대칭 키 자체는 게시자와 구독자에서 다른 방법으로 보안을 설정할 수 있습니다.  
  
### <a name="to-create-and-replicate-encrypted-column-data"></a>암호화된 열 데이터를 만들고 복제하려면  
  
1.  게시자에서 [CREATE SYMMETRIC KEY](/sql/t-sql/statements/create-symmetric-key-transact-sql)를 실행합니다.  
  
    > [!IMPORTANT]  
    >  KEY_SOURCE 값은 대칭 키를 다시 만들고 데이터를 해독하는 데 사용할 수 있는 중요한 데이터입니다. KEY_SOURCE는 항상 안전하게 저장하고 전송해야 합니다.  
  
2.  [OPEN SYMMETRIC KEY](/sql/t-sql/statements/open-symmetric-key-transact-sql) 를 실행하여 새 키를 엽니다.  
  
3.  [EncryptByKey](/sql/t-sql/functions/encryptbykey-transact-sql) 함수를 사용하여 게시자에서 열 데이터를 암호화합니다.  
  
4.  [CLOSE SYMMETRIC KEY](/sql/t-sql/statements/close-symmetric-key-transact-sql) 를 실행하여 키를 닫습니다.  
  
5.  암호화된 열이 있는 테이블을 게시합니다. 자세한 내용은 [Create a Publication](../publish/create-a-publication.md)를 참조하세요.  
  
6.  게시를 구독합니다. 자세한 내용은 [끌어오기 구독 만들기](../create-a-pull-subscription.md) 또는 [밀어넣기 구독 만들기](../create-a-push-subscription.md)를 참조하세요.  
  
7.  구독을 초기화합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
8.  ALGORITHM, KEY_SOURCE 및 IDENTITY_VALUE에 대해 1단계와 동일한 값을 사용하여 구독자에서 [CREATE SYMMETRIC KEY](/sql/t-sql/statements/create-symmetric-key-transact-sql) 를 실행합니다. ENCRYPTION BY에는 다른 값을 지정할 수 있습니다.  
  
    > [!IMPORTANT]  
    >  KEY_SOURCE 값은 대칭 키를 다시 만들고 데이터를 해독하는 데 사용할 수 있는 중요한 데이터입니다. KEY_SOURCE는 항상 안전하게 저장하고 전송해야 합니다.  
  
9. [OPEN SYMMETRIC KEY](/sql/t-sql/statements/open-symmetric-key-transact-sql) 를 실행하여 새 키를 엽니다.  
  
10. 구독자에서 [DecryptByKey](/sql/t-sql/functions/decryptbykey-transact-sql) 함수를 사용하여 복제된 데이터를 해독합니다.  
  
11. [CLOSE SYMMETRIC KEY](/sql/t-sql/statements/close-symmetric-key-transact-sql) 를 실행하여 키를 닫습니다.  
  
## <a name="example"></a>예제  
 이 예에서는 대칭 키, 대칭 키의 보안 설정에 사용되는 인증서 및 마스터 키를 만듭니다. 이러한 키는 게시 데이터베이스에서 생성됩니다. 그런 다음 `SalesOrderHeader` 테이블에서 암호화된 열(EncryptedCreditCardApprovalCode)을 만드는 데 사용됩니다. 이 열은 암호화되지 않은 CreditCardApprovalCode 열 대신 AdvWorksSalesOrdersMerge 게시에 게시됩니다. 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
 [!code-sql[HowTo#sp_PublishEncryptedColumn](../../../snippets/tsql/SQL15/replication/howto/tsql/publishencryptedcolumn.sql#sp_publishencryptedcolumn)]  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepub.sql#sp_addmergearticle)]  
  
## <a name="example"></a>예제  
 이 예에서는 첫 번째 예의 ALGORITHM, KEY_SOURCE 및 IDENTITY_VALUE에 동일한 값을 사용하여 구독 데이터베이스에서 같은 대칭 키를 다시 만듭니다. 암호화된 열을 복제하기 위해 AdvWorksSalesOrdersMerge 게시에 대한 구독을 이미 초기화했다고 가정합니다. 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 스크립트 파일에 자격 증명을 저장해야 하는 경우에는 저장 및 전송 중에 무단으로 액세스하지 못하도록 파일에 보안을 설정해야 합니다.  
  
 [!code-sql[HowTo#sp_SubscriberEncryptedColumn](../../../snippets/tsql/SQL15/replication/howto/tsql/subscriberencryptedcolumn.sql#sp_subscriberencryptedcolumn)]  
  
## <a name="see-also"></a>관련 항목  
 [보안 개요&#40;복제&#41;](security-overview-replication.md)   
 [두 서버에서 동일한 대칭 키 만들기](../../security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
  
