---
title: "Các bài blogs đã đăng"
date: 2026-07-31
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Tại đây sẽ là phần liệt kê, giới thiệu các blogs mà các bạn đã đăng trên [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj).

###  [Blog 1 - XỬ LÝ LỖI RACE CONDITION TRONG HỆ THỐNG GIAO DỊCH SERVERLESS VỚI AMAZON DYNAMODB](3.1-Blog1/)
Blog này chia sẻ bài toán thực tế mà nhóm gặp phải trong dự án NaturEra Green Banking khi các request thanh toán đồng thời gây ra sai lệch số dư. Qua đó, bài viết giới thiệu giải pháp đẩy việc quản lý toàn vẹn dữ liệu xuống tầng Database bằng cách sử dụng `ConditionExpression` và `TransactWriteItems` của Amazon DynamoDB để triệt tiêu hoàn toàn Race Condition trong kiến trúc Serverless.