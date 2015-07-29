---
published: true
title: ARJUNA016051: Thread is already associated with a transaction!
layout: post
---
This issue occurs when someone tries to begin a transaction in bean managed transaction process and previous tx is still in process or hung without either committing or rolling back.

I have experienced this issue while working on a transaction based web service application. In order to resolve this, I would recommend to check the status of the transaction object created. Add below lines of code before beginning a transaction,  in order to resolve this issue.

int txStatus = transaction.getStatus();
if (txStatus == Status.STATUS_MARKED_ROLLBACK || txStatus == Status.STATUS_ROLLEDBACK) {
                logger.warn("Rolling back the transaction");
                transaction.rollback();
} 