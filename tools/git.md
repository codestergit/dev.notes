# git

#Delete local tags.
git tag -l | xargs git tag -d
#Fetch remote tags.
git fetch
#Delete remote tags.
git tag -l | xargs -n 1 git push --delete origin

上下箭头选择log的版本
enter进入具体版本查看详细
k和j是上下滚动查看详细信息的内容
m是关闭详细信息，返回到log的版本
pageup/pagedown是同k和j，只不过是一屏一屏的滚动