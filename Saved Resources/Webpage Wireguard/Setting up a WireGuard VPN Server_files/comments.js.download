// https://p3lim.net/2018/05/04/github-powered-comments

const article = document.querySelector('article');
const nwo = article.getAttribute('data-nwo'); // site.github.repository_nwo
const sha = article.getAttribute('data-sha'); // page.sha (custom front-matter)

let get = url => {
	// Promise-based XMLHttpRequest
	return new Promise((resolve, reject) => {
		let xhr = new XMLHttpRequest();
		xhr.onerror = () => reject(xhr.statusText);
		xhr.onload = () => (xhr.status === 200) ? resolve(xhr.response) : reject(xhr.statusText);
		xhr.open('GET', url);
		xhr.send();
	});
};

let template = comment => {
	// returns HTML markup based on template interpolated with data
	let time = moment(comment.created_at);
	return `
		<div ${comment.author_association === 'OWNER' ? `class='author'` : ''}>
			<div class='avatar'>
				<a href='${comment.user.html_url}'>
					<img alt='@${comment.user.login}' src='${comment.user.avatar_url}'>
				</a>
			</div>
			<div class='comment'>
				<div class='header'>
					<h3>
						<strong>
							<a href='${comment.user.html_url}'>${comment.user.login}</a>
						</strong>
						commented
						<a class='timestamp' href='${comment.html_url}'>
							<relative-time datetime='${comment.created_at}' title='${time.format('MMM D, YYYY, HH:mm')}'>${time.fromNow()}</relative-time>
						</a>
					</h3>
				</div>
				<div class='body gfm'>
					${marked(comment.body, {gfm: true})}
				</div>
			</div>
		</div>
	`;
};

// query for the comments section
let section = document.querySelector('article #comments');

// hide temp text
document.querySelector('article #comments > span').style.display = 'none';

// request comments for article from GitHub
get(`https://api.github.com/repos/${nwo}/commits/${sha}/comments`)
	.then(data => {
		// parse comments as HTML and append to comments section
		section.insertAdjacentHTML('beforeend', JSON.parse(data).map(template).join(''));

		// append link to commit to comments section
		section.insertAdjacentHTML('beforeend', `<div class='gfm'><a href='https://github.com/${nwo}/commit/${sha}#comments'>Leave a comment on GitHub</a></div>`);
	})
	.catch(error => {
		// append error message to comment section
		section.insertAdjacentHTML('beforeend', '<div class="gfm"><p>Failed to fetch comments :(</p></div>');
	});
