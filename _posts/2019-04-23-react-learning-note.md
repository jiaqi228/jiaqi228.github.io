---
title: "React学习笔记：State覆盖问题"
categories:
  - React
  - Learning Note
tags:
  - React
  - Learning Note
---

关于React中的State（状态）管理，在学习时遇到了一些问题，后经解决特此记录。

纯粹的React中，State是在Component（组件）中进行管理的。Component其实分为Stateful和Stateless，Stateful就是通过createReactClass或者extends React.Component的方法创建的组件；Stateless是通过函数/方法创建的组件。

State的管理只能在 **Stateful** 的Component中进行。

Stateful（createReactClass）：
```javascript
const StarRating = createClass({
    displayName: 'StarRating',
    propTypes: {
        totalStars: PropTypes.number
    },
    getDefaultProps() {
        return {
            totalStars: 5
        }
    },
    getInitialState() {
        return {
            starsSelected: 0
        }
    },
    change(starsSelected) {
        this.setState({ starsSelected })
    },
    render() {
        const { totalStars } = this.props
        const { starsSelected } = this.state
        return (
            <div className="star-rating">
                {[...Array(totalStars)].map((n, i) =>
                    <Star key={i}
                        selected={i < starsSelected}
                        onClick={() => this.change(i + 1)}
                    />
                )}
                <p>{starsSelected} of {totalStars} stars</p>
            </div>
        )
    }
})
```
> createReactClass创建Component的方法好像已经不被推荐。

Stateful（extends React.Component）：
```javascript
class StarRating extends Component {
    constructor(props) {
        super(props)
        this.state = {
            starsSelected: 0
        }
        this.change = this.change.bind(this)
    }
    change(starsSelected) {
        this.setState({ starsSelected })
    }
    render() {
        const { totalStars } = this.props
        const { starsSelected } = this.state
        return (
            <div className="star-rating">
                {[...Array(totalStars)].map((n, i) =>
                    <Star key={i}
                        selected={i < starsSelected}
                        onClick={() => this.change(i + 1)}
                    />
                )}
                <p>{starsSelected} of {totalStars} stars</p>
            </div>
        )
    }
}

StarRating.propTypes = {
    totalStars: PropTypes.number
}

StarRating.defaultProps = {
    totalStars: 5
}
```


Stateless（Function）：
```javascript
const Star = ({ selected = false, onClick = f => f }) =>
    <div className={(selected) ? "star selected" : "star"}
        onClick={onClick}>
    </div>
Star.propTypes = {
    selected: PropTypes.bool,
    onClick: PropTypes.func
}
```

在学习过程中试着制作了一个纯粹React的APP：
- Index.js render App
- App 是Stateful的Component
- App 中使用2个Component: AddColorForm 和 ColorList
- AddColorForm 是Stateful的Component
- ColorList 是Stateful的Component

在使用App时发现动作可以正常运行，但是State并没有被保持住，每次画面刷新都会清空State。经过不断地尝试/观察作者的代码，意识到了Stateful和Stateless的区别。由于AddColorForm和ColorList都是Stateful的Component，导致这2个Component的State覆盖了App的State。

以下的测试清空都会导致State无法正确管理：
1. AddColorForm是Stateful & ColorList是Stateful
2. AddColorForm是Stateful & ColorList是Stateless
3. AddColorForm是Stateless & ColorList是Statefull

由于还在学习React，还没有接触到更深层的内容（比如在Stateful的Component中传递State？State管理中间件？等等），所以理解如上。