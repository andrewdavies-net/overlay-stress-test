docker build --target compile-image --tag compile-image:0.0.1 .

You can tag intermediate stage alongside target this makes it easier to refer back to later as buildah doesnt cache intermediate layers like docker does

https://github.com/containers/buildah/issues/4612#issuecomment-1455526295
https://stackoverflow.com/questions/58971382/how-to-give-name-or-tag-for-intermediate-image