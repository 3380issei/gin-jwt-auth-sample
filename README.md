## やりたいこと
Ginでユーザーログイン機能を実装し、ログインユーザーだけがアクセス可能なエンドポイントをJWT認証を使って実装したい。

### ```main.go```
```go
func main() {
	r := gin.Default()

	r.POST("/login", loginHandler)

	authGroup := r.Group("/auth")
	authGroup.Use(authMiddleware)
	authGroup.GET("/", func(c *gin.Context) {
		c.JSON(http.StatusOK, gin.H{"message": "you are authorized"})
	})

	r.Run(":8080")
}
```

- ```POST``` ```/login```：ログイン時にアクセスするエンドポイント
- ```GET``` ```/auth```：ログインユーザーしかアクセスできない

```/auth```が付くエンドポイントをグループ化し、middlewareを用いて、ログインユーザーのみアクセスできるようにしてます。

## 参考
https://developer.mamezou-tech.com/blogs/2022/12/08/jwt-auth/
