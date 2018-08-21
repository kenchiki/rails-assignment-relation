# 2つのモデルの関連からデータを引き出せるようになる

## 実行手順
- `bundle exec rake db:create`
- `bundle exec rake db:migrate`
- `bundle exec rails c`

```ruby
# Entryを登録
entry1 = Entry.create(title: 'はじめてのエントリー', body: 'はじめまして！')
entry2 = Entry.create(title: '2番目のエントリー', body: 'おひさしぶりです！')
entry3 = Entry.create(title: '3番目のエントリー', body: 'もうくじけました・・・')

# Commentを登録
entry1.comments.create(body: 'てすてす', status: 'approved')
entry1.comments.create(body: 'どうもどうも', status: 'unapproved')
entry3.comments.create(body: 'こんにちはこんにちは！', status: 'approved')

# Entryのid:1(title:はじめてのエントリー)に紐づくCommentを表示
Entry.find(1).comments

# statusがunapprovedであるCommentがあるEntryを表示
Entry.joins(:comments).where(comments: {status: 'unapproved'})
```

## Ruby version
2.5.1
