■参考
https://github.com/TimingJL/movie_review


■newとbuildの違い（Ruby on Rails）
https://ryoutaku-jo.hatenablog.com/entry/2019/03/28/new%E3%81%A8build%E3%81%AE%E9%81%95%E3%81%84%EF%BC%88Ruby_on_Rails%EF%BC%89


■Paper Clip で Image content type is invalid
https://qiita.com/Yinaura/items/228fba6d0523dfe00ee3
https://stackoverflow.com/questions/19902426/paperclips-content-type-is-invalid-according-to-app-but-isnt

■Rails DBコマンド
https://qiita.com/k-o-u/items/a9b5e5472ba8415dd1aa

■movie_length が反映されない
`movie`を`moive`と誤って入力していたことが問題

### 1.rails db コマンドで問題を特定
```
rails db
sqlite> .table
sqlite> .schema movie
```
### 2.migrateファイル変更&再度migrate
`/movie_review/db/migrate` のmoive を movieに修正
`rails db:migrate:reset`
### 3.Viewファイル修正
`/movie_review/app/views/movies/_form.html.erb`を修正
```
  <div class="field">
    <%= form.label :moive_length %>
    <%= form.text_field :movie_length %>
  </div>
↓
  <div class="field">
    <%= form.label :movie_length %>
    <%= form.text_field :movie_length %>
  </div>
```
### 4.コントローラを修正
`/movie_review/app/controllers/movies_controller.rb`を修正
```
    def movie_params
      params.require(:movie).permit(:title, :description, :moive_length, :director, :rating, :image)
    end
↓
    def movie_params
      params.require(:movie).permit(:title, :description, :movie_length, :director, :rating, :image)
    end
```


■Raty
https://github.com/wbotelhos/raty
https://qiita.com/yuforest/items/2686960f0a43ec2caa5b
https://qiita.com/kitaokeita/items/1e40724c3384507cec13
https://www.tech-tech.xyz/5299581.html

Ratya.jsが上手く機能しない。。。
http://gouf.hatenablog.com/entry/2018/02/05/003548

■Seach Kick
https://github.com/ankane/searchkick
https://qiita.com/terappy/items/537c069923144a9d9755

■Elastic Search
https://qiita.com/ekzemplaro/items/acc81bc96fdd56eed587
